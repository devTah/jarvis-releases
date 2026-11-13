# Jarvis releases

Installers and the update manifest (`latest.json`) for Jarvis, a personal desktop assistant.
Each release contains the Windows installer, its updater signature (`.sig`) and `latest.json`.
The installed app checks
`https://github.com/devTah/jarvis-releases/releases/latest/download/latest.json` for updates and
installs only builds signed with the Jarvis updater key.

The source code is not in this repository.
