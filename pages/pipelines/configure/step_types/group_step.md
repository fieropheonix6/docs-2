# Group step

A group step can contain various sub-steps, and display them in a single logical group on the Build page.

For example, you can group all of your linting steps or all of your UI test steps to keep the Build page less messy. Sub-groups and nested groups are not supported.

The group step also helps manage dependencies between a collection of steps, for example, "step X" [`depends_on`](/docs/pipelines/configure/step-types/group-step#group-step-attributes) everything in "group Y".

A group step can be defined in your pipeline settings or your [pipeline.yml](/docs/pipelines/configure/defining-steps) file.

Here is an example of using the group step:

```yml
steps:
  - group: "\:lock_with_ink_pen\: Security Audits"
    key: "audits"
    steps:
      - label: "\:brakeman\: Brakeman"
        command: ".buildkite/steps/brakeman"
      - label: "\:bundleaudit\: Bundle Audit"
        command: ".buildkite/steps/bundleaudit"
      - label: "\:yarn\: Yarn Audit"
        command: ".buildkite/steps/yarn"
      - label: "\:yarn\: Outdated Check"
        command: ".buildkite/steps/outdated"
```
{: codeblock-file="pipeline.yml"}

This is how it's displayed in the UI:

<%= image "job-groups-in-UI.png", width: 1760, height: 436, alt: "Job groups displayed in the Buildkite UI" %>

Only the first 50 jobs within a build header can ever be displayed in the UI, so you might not see all of your groups at all times. However, the jobs are fine and will still show up on the build page.


## Group step attributes

Required attributes:

<table data-attributes>
<tr>
    <td><code>group</code></td>
    <td>
      Name of the group in the UI. In YAML, if you don't want a label, pass a `~`. Can also be provided in the `label` attribute if `null` is provided to the `group` attribute.<br/>
      <em>Type:</em> <code>string</code> or <code>null</code>
    </td>
  </tr>
  <tr>
    <td><code>steps</code></td>
    <td>
      A list of steps in the group; at least 1 step is required. Allowed step types: <a href="/docs/pipelines/configure/step-types/wait-step"><code>wait</code></a>, <a href="/docs/pipelines/configure/step-types/trigger-step"><code>trigger</code></a>, <a href="/docs/pipelines/configure/step-types/command-step"><code>command</code>/<code>commands</code></a>, <a href="/docs/pipelines/configure/step-types/block-step"><code>block</code></a>, <a href="/docs/pipelines/configure/step-types/input-step"><code>input</code></a>.<br/>
      <em>Type:</em> <code>array</code>
    </td>
  </tr>
</table>

Optional attributes:

<table data-attributes>
  <tr>
    <td><code>allow_dependency_failure</code></td>
    <td>
      Whether to continue to run this step if any of the steps named in the <code>depends_on</code> attribute fail.<br/>
      <em>Default:</em> <code>false</code>
    </td>
  </tr>
  <tr>
    <td><code>depends_on</code></td>
    <td>
      A list of step or group keys that this step depends on. This step or group will only run after the named steps have completed. See <a href="/docs/pipelines/configure/dependencies">managing step dependencies</a> for more information.<br/>
      <em>Example:</em> <code>"test-suite"</code>
    </td>
  </tr>
  <tr>
    <td><code>if</code></td>
    <td>
      A boolean expression that omits the step when false. See <a href="/docs/pipelines/configure/conditionals">Using conditionals</a> for supported expressions.<br/>
      <em>Example:</em> <code>build.message != "skip me"</code>
    </td>
  </tr>
  <tr>
    <td><code>key</code></td>
    <td>
      A unique string to identify the step, block, or group.<br/>
      Keys can not have the same pattern as a UUID (<code>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</code>).<br/>
      <em>Example:</em> <code>"test-suite"</code><br/>
      <em>Alias:</em> <code>identifier</code>
    </td>
  </tr>
  <tr>
    <td><code>label</code></td>
    <td>
      The label that will be displayed in the pipeline visualisation in Buildkite (name of the group in the UI). Supports emoji.<br/>
      <em>Example:</em> <code>"\:hammer\: Tests" will be rendered as ":hammer: Tests"</code><br/>
    </td>
  </tr>
  <tr>
    <td><code>notify</code></td>
    <td>
      Allows you to <a href="/docs/pipelines/configure/notifications">trigger</a> build notifications to different services. You can also choose to conditionally send notifications based on pipeline events.<br/>
      <em>Example:</em> <code>"github_commit_status:"</code><br/>
    </td>
  </tr>
  <tr>
    <td><code>skip</code></td>
    <td>
      Whether to skip this step or not. Passing a string provides a reason for skipping this command. Passing an empty string is equivalent to <code>false</code>.
      Note: Skipped steps will be hidden in the pipeline view by default, but can be made visible by toggling the 'Skipped jobs' icon.<br/>
      <em>Example:</em> <code>true</code><br/>
      <em>Example:</em> <code>false</code><br/>
      <em>Example:</em> <code>"My reason"</code>
    </td>
  </tr>
</table>

## Agent-applied attributes

<%= render_markdown partial: 'pipelines/configure/step_types/agent_applied_attributes' %>

## Parallel groups

If you put two or more group steps in a YAML config file consecutively, they will run in parallel. For example:

```yml
# 1.sh and 3.sh will start at the same time.
# 2.sh will start when 1.sh finishes, and 4.sh will start
# when 3.sh finishes.
steps:
  - group: "first"
    steps:
      - command: "1.sh"
      - wait
      - command: "2.sh"
  - group: "second"
    steps:
      - command: "3.sh"
      - wait
      - command: "4.sh"
```
{: codeblock-file="pipeline.yml"}

Running jobs in parallel has some limitations:

<!-- vale off -->
* Parallel groups will be displayed ungrouped if the build's jobs are truncated because Buildkite doesn't currently store or calculate any information about the number of jobs in a non-parallel group.
* If a parallel step exists within a group, parallel jobs are treated as regular jobs within a step group - so you can't have parallel groups within step groups. So, for example, a `group` that contains two `steps` each with `parallel: 4` will display eight jobs in it, with no visual indication that those eight jobs are two parallel steps.

<!-- vale on -->

* If a parallel job group is within a named group, the groups are handled as though the parallel group isn't there.
* It's impossible to have a parallel job with only some of the jobs within a group, as they're all created on the same YAML step entry.

## Using wait steps in job groups

You can have [wait steps](/docs/pipelines/configure/step-types/wait-step) in a group. Such steps operate independently of other groups. For example, both groups will operate independently here, meaning `d.sh` won't wait on `a.sh` to finish. Note also that wait steps are counted in the group step total, so both `Group01` and `Group02` contain 3 steps.

```yml
steps:
  - group: "Group01"
    depends_on: "tests"
    steps:
      - command: "a.sh"
      - wait
      - command: "b.sh"

  - group: "Group02"
    depends_on: "tests"
    id: "toast"
    steps:
      - command: "c.sh"
      - wait
      - command: "d.sh"

  - command: "yay.sh"
    depends_on: "toast"
```
{: codeblock-file="pipeline.yml"}

## Group merging

If you upload a pipeline that has a `group` or `label` that matches the group of the step that uploaded it, those groups will be merged together in the Buildkite UI.

This merging behavior only applies if the group step with the matching `group` or `label` is the first step within the uploaded pipeline.

Note that inside a single pipeline, groups with the same `group` or `label` will not be merged in the Buildkite UI.

> 📘 You can't define the same key twice
> Trying to create different groups or steps with the same `key` attribute will result in an error.

For example, you have a YAML file:

```yml
steps:
  - group: "Setup"
    steps:
      - commands:
        - "buildkite-agent pipeline upload"
        - echo "start"
```
{: codeblock-file="pipeline.yml"}

And this YAML file uploads a pipeline that has a group with the same name:

```yml
steps:
  - group: "Setup"
    steps:
      - command: "docker build"
```
{: codeblock-file="pipeline.yml"}

These groups will be merged into one in the UI, and the `docker build` step will be added to the existing group.

Similarly, if you have a YAML file:

```yml
steps:
  - group: ~
    label: "Setup"
    steps:
      - commands:
        - "buildkite-agent pipeline upload"
        - echo "start"
```
{: codeblock-file="pipeline.yml"}

And this YAML file uploads a pipeline that has a group with the same label:

```yml
steps:
  - group: ~
    label: "Setup"
    steps:
      - command: echo "proceed"
```
{: codeblock-file="pipeline.yml"}

These groups will be merged into one in the UI, and the `echo "proceed"` step will be added to the existing group.

## Example

<a class="Docs__example-repo" href="https://github.com/buildkite/group-step-example">
 <span class="icon">:buildkite:</span>
  <span class="detail">
    <strong>Group steps</strong>
     <span class="description">An example of how to group steps in a pipeline</span>
    <span class="repo">github.com/buildkite/group-step-example</span>
  </span>
</a>
