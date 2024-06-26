---
#  _____   ____    _   _  ____ _______   ______ _____ _____ _______
#  |  __  / __   |  | |/ __ __   __| |  ____|  __ _   _|__   __|
#  | |  | | |  | | |  | | |  | | | |    | |__  | |  | || |    | |
#  | |  | | |  | | | . ` | |  | | | |    |  __| | |  | || |    | |
#  | |__| | |__| | | |  | |__| | | |    | |____| |__| || |_   | |
#  |_____/ ____/  |_| _|____/  |_|    |______|_____/_____|  |_|
#  This file is auto-generated by script/generate_graphql_api_content.sh,
#  please build the schema.graphql by running `rails graphql:update_reference_schema`
#  with https://github.com/buildkite/buildkite/,
#  replace the content in data/schema.graphql
#  and run the generation script `./scripts/generate-graphql-api-content.sh`.

title: RepositoryProviderBitbucketServerSettings – Objects – GraphQL API
toc: false
---
<!-- vale off -->
<h1 class="has-pills">
  RepositoryProviderBitbucketServerSettings
  <span data-algolia-exclude><span class="pill pill--object pill--normal-case pill--large"><code>OBJECT</code></span></span>
</h1>
<!-- vale on -->


Settings for Bitbucket Server repository

<table class="responsive-table responsive-table--single-column-rows">
  <thead>
    <th>
      <h2 data-algolia-exclude>Fields</h2>
    </th>
  </thead>
  <tbody>
    <tr><td><h3 class="is-small has-pills"><code>buildBranches</code><a href="/docs/apis/graphql/schemas/scalar/boolean" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR Boolean"><code>Boolean!</code></a></h3><p>Whether to create builds when branches are pushed.</p></td></tr><tr><td><h3 class="is-small has-pills"><code>buildPullRequests</code><a href="/docs/apis/graphql/schemas/scalar/boolean" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR Boolean"><code>Boolean!</code></a></h3><p>Whether to create builds for commits that are part of a Pull Request.</p></td></tr><tr><td><h3 class="is-small has-pills"><code>buildTags</code><a href="/docs/apis/graphql/schemas/scalar/boolean" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR Boolean"><code>Boolean!</code></a></h3><p>Whether to create builds when tags are pushed.</p></td></tr><tr><td><h3 class="is-small has-pills"><code>filterCondition</code><a href="/docs/apis/graphql/schemas/scalar/string" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR String"><code>String</code></a></h3><p>The conditions under which this pipeline will trigger a build.</p></td></tr><tr><td><h3 class="is-small has-pills"><code>filterEnabled</code><a href="/docs/apis/graphql/schemas/scalar/boolean" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR Boolean"><code>Boolean</code></a></h3><p>Whether the filter is enabled</p></td></tr>
  </tbody>
</table>




<h2 data-algolia-exclude>Interfaces</h2>
<div>
  <a href="/docs/apis/graphql/schemas/interface/repositoryprovidersettings" class="pill pill--interface pill--normal-case pill--large" title="Go to INTERFACE RepositoryProviderSettings">
  <code>RepositoryProviderSettings</code>
</a>

</div>
