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

title: ClusterToken – Objects – GraphQL API
toc: false
---
<!-- vale off -->
<h1 class="has-pills">
  ClusterToken
  <span data-algolia-exclude><span class="pill pill--object pill--normal-case pill--large"><code>OBJECT</code></span></span>
</h1>
<!-- vale on -->


A token used to connect an agent in cluster to Buildkite

<table class="responsive-table responsive-table--single-column-rows">
  <thead>
    <th>
      <h2 data-algolia-exclude>Fields</h2>
    </th>
  </thead>
  <tbody>
    <tr><td><h3 class="is-small has-pills"><code>allowedIpAddresses</code><a href="/docs/apis/graphql/schemas/scalar/string" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR String"><code>String</code></a></h3><p>A list of CIDR-notation IPv4 addresses from which agents can use this token. Please note that this feature is not yet available to all organizations</p></td></tr><tr><td><h3 class="is-small has-pills"><code>cluster</code><a href="/docs/apis/graphql/schemas/object/cluster" class="pill pill--object pill--normal-case pill--medium" title="Go to OBJECT Cluster"><code>Cluster</code></a></h3></td></tr><tr><td><h3 class="is-small has-pills"><code>createdBy</code><a href="/docs/apis/graphql/schemas/object/user" class="pill pill--object pill--normal-case pill--medium" title="Go to OBJECT User"><code>User</code></a></h3></td></tr><tr><td><h3 class="is-small has-pills"><code>description</code><a href="/docs/apis/graphql/schemas/scalar/string" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR String"><code>String</code></a></h3><p>A description about what this cluster agent token is used for</p></td></tr><tr><td><h3 class="is-small has-pills"><code>expiresAt</code><a href="/docs/apis/graphql/schemas/scalar/datetime" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR DateTime"><code>DateTime</code></a></h3><p>The date and time at which this token will expire and no longer be valid. If empty, the token will never expire.</p></td></tr><tr><td><h3 class="is-small has-pills"><code>id</code><a href="/docs/apis/graphql/schemas/scalar/id" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR ID"><code>ID!</code></a></h3></td></tr><tr><td><h3 class="is-small has-pills"><code>token</code><a href="/docs/apis/graphql/schemas/scalar/string" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR String"><code>String!</code></a><span class="pill pill--deprecated"><code>deprecated</code></span></h3><p><em>Deprecated: Hiding these after creation to improve security. Use the `token_value` field on ClusterAgentTokenCreate instead.</em></p><p>The token value used to register a new agent to this tokens cluster. This will soon return an empty string before we finally remove this field.</p></td></tr><tr><td><h3 class="is-small has-pills"><code>uuid</code><a href="/docs/apis/graphql/schemas/scalar/id" class="pill pill--scalar pill--normal-case pill--medium" title="Go to SCALAR ID"><code>ID!</code></a></h3><p>The public UUID for this cluster token</p></td></tr>
  </tbody>
</table>




<h2 data-algolia-exclude>Interfaces</h2>
<div>
  <a href="/docs/apis/graphql/schemas/interface/node" class="pill pill--interface pill--normal-case pill--large" title="Go to INTERFACE Node">
  <code>Node</code>
</a>

</div>
