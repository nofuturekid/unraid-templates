# unraid-templates

Unraid Community Applications (CA) templates by nofuturekid. MIT licensed (templates and docs only; the applications have their own licenses).

| Template | Application |
| --- | --- |
| [templates/tasmofleet.xml](templates/tasmofleet.xml) | [tasmofleet](https://github.com/nofuturekid/tasmofleet), Tasmota fleet manager |

## Manual install (before it is listed in CA)

Copy the file to `/boot/config/plugins/dockerMan/templates-user/my-tasmofleet.xml`, then Docker -> Add Container -> select `TasmoFleet`.

Notes on the tasmofleet template:

- Defaults need no configuration: HTTPS web UI with a self-signed certificate on port 8443; the first admin password is in `initial-admin-password` in the appdata folder.
- The container runs as UID/GID 65532, not `nobody` (99:100). Run `chown -R 65532:65532 /mnt/user/appdata/tasmofleet` once.
- Tasmota devices download firmware over plain HTTP from the "Firmware server" port (container port 80, default host port 8081, because host port 80 is the Unraid WebGUI). Enter `http://SERVER-IP:8081/` as the firmware URL on tasmofleet's System settings page.
- Behind a reverse proxy: set Trusted proxies and Public URL, set Self-signed TLS to `false`, UI listen to `:8080` and the Web UI container port to `8080`, and use your proxy URL as WebUI.

## Submitting (maintainer checklist)

1. Forum support thread: Unraid forum -> Docker Containers (https://forums.unraid.net/forum/58-docker-containers/) -> new topic, title `[Support] nofuturekid - TasmoFleet`. First post: short description, link to the GitHub project and the template, install notes from above. Copy the topic URL.
2. Put that URL into `<Support>` in `templates/tasmofleet.xml` (replacing the GitHub issues link) and add `<Forum>TOPIC_URL</Forum>` to `ca_profile.xml`. Commit and push.
3. Open https://ca.unraid.net/submit/new, sign in with the Unraid account, paste `https://github.com/nofuturekid/unraid-templates` as GitHub URL, run the review, fix reported issues, confirm the submission.
4. Requirements checked by the form: public and active repo, OSI license (MIT, present), valid template XML, non-empty `<Profile>` in `ca_profile.xml` (present).
5. After approval, CA picks template changes up from this repo automatically; just push updates to `main`.

Validate locally: `xmllint --noout templates/*.xml ca_profile.xml`.
