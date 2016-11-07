## JupyterHub

### Not tied to releases

JupyterHub constellation of repos may move to top-level jupyterhub org on GitHub.

- jupyterhub itself
- spawners
- authenticators
- reference deployments
- configurable-http-proxy

#### Reference Deployments

Start with two reference deployments:

- common best practices
    - letsencrypt
    - nginx out front
    - postgres for db
- single machine nbgrader, no docker
    - ansible
    - local users, optionally GitHub auth
    - based on Brian's https://github.com/calpolydatascience/jupyterhub-deploy-data301
- docker, no nbgrader
    - docker-compose
    - GitHub OAuth


### Next (0.7)

The main feature of 0.7 will be the addition of Services.

- A Service is a process that interacts with JupyterHub and is managed by the Hub process.
- A service MAY:
   - use the Hub REST API with an authentication token
   - run an HTTP server that is added to the Hub proxy
   - authenticate HTTP requests with GitHub users in a manner similar to the single-user server
- Enhancements will include:
   - The ability to launch services, provided an auth token for the REST API as a specified user
   - An importable implementation of authentication with the Hub
- Examples:
   - `cull_idle_servers` example script which shuts down servers that have been idle for a period of time
    - uses Hub REST API as an administrator for starting
   - nbgrader formgrader
     - uses Hub auth to specify graders
  - Hub statistics (compmodels/stats)


### Next + 1 (0.8)

The main feature of 0.8 will be the addition of a sharing service.

Users should be able to:

- Push a project to other users.
- Get a checkout of a project from other users.
- Push updates to a published project.
- Pull updates from a published project.
- Manage conflicts/merges by simply picking a version (our/theirs)
- Get a checkout of a project from the internet. These steps are completely different from saving notebooks/files.
- Have directories that are managed by git completely separately from our stuff.
- Look at pushed content that they have access to without an explicit pull.
- Define and manage teams of users.
  - Adding/removing a user to/from a team gives/removes them access to all projects that team has access to.
- Build other services, such as static HTML publishing and dashboarding on top of these things.
- Enter into real-time collaboration mode for a project that starts a shared execution context.

### Future

- Once the single-user notebook package supports realtime collaboration,
  implement sharing mechanism integrated into the Hub.
