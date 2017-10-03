## JupyterHub

### HubShare

HubShare will be a sharing service for use with JupyterHub.

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


### Next (0.9)

JupyterHub will also add some features relating to resource monitoring and management:

- (prometheus?) API for resource monitoring
- tracking activity on single-user servers instead of the proxy
- notes and activity tracking per API token
- UI for managing named servers

### Future

- Enter into real-time collaboration mode for a project that starts a shared execution context.
- Once the single-user notebook package supports realtime collaboration,
  implement sharing mechanism integrated into the Hub.

