# Changelog

All important changes to this role are listed here.

## [1.0.3] - 2026-10-26

- **The role could not configure any user on ansible-core 2.20.** `with_items` over the `awscli_users` dictionary handed the whole dictionary to the task as a single item instead of its keys, so `getent` received the dictionary as the user name and failed with `One or more supplied key could not be found in the database`. The loop now iterates over the sorted keys of the dictionary with `loop`.
- **The failure printed the credentials.** The error message includes the module parameters, and the parameter was the full `awscli_users` structure with the access key and the secret. Fixing the loop removes that path, and the two template tasks that write `credentials` and `config` now run with `no_log: true` and `diff: false`, so a failure while rendering them cannot leak the secret either. A host that already hit the error should have the key rotated.
- **Internal variables were renamed.** The loop variable `_user` is now `__awscli_user`, and the registered result and the home path facts carry the same `__awscli_` prefix, as the project lint rules require. They are internal and not meant to be overridden, but a playbook that read `_user` from this role needs the new name. The templates use `__awscli_user` as well.
- **One-item loops were removed.** The file, template and `getent` tasks looped over a list holding only the current user; they now use the loop variable directly. File modes are quoted strings.
- **`meta/main.yml` follows the project format.** Company, description, `min_ansible_version` 2.20 (the role is validated against ansible-core 2.20), the Debian platform and the `awscli` tag were added, and the `namespace` field was dropped.
