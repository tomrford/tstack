tstack is a growing collection of skills for maintaining many projects of varying scope, intended to become a public ChatGPT plugin.
Start with focused guidance on testing and validation; develop broader workflows from real project work, pstack and experience with dots and orchestrator chats.
Keep skills concise, practical and grounded in demonstrated needs.

Commit and push changes directly to `main`; do not open PRs for this repository unless explicitly requested.

Track the release version in `plugin.json`. Before publishing an update, compare the repository and saved plugin versions, bump the patch above both, and commit the version with the changes. Publish that committed version; do not rely on the publisher's automatic bump. Verify the repository and saved plugin versions agree after syncing.

After pushing changes to `main`, if Plugin Creator is available, check for an existing personal tstack plugin owned by the current user. Verify its source matches this repository; a loaded plugin or matching name alone is insufficient. Updating a verified match is authorised as part of completing delivery. Preserve its identity and audience. If no match exists, skip syncing; if several match, ask which to update. Do not create a replacement plugin.
Use Plugin Creator's update-plugin skill to read the current source and release ID, publish the manifest and skills from the exact pushed commit, and explicitly remove packaged files deleted from the source. Publisher-generated files follow the publisher's lifecycle. Verify the saved version and affected files, report the plugin link, and remind the user to start a new chat. If syncing is unavailable or fails, report that outcome.
