---
name: sync-docs
description: Update project documentation to reflect changes and maintain a concise, searchable changelog. Use when the user asks to sync docs, update a README based on changes, document modifications, or update a changelog.
license: MIT
---

# sync-docs

Explain the project's current state after a change and leave a useful record for future reference. Follow the user's scope and the project's documentation conventions; keep the result as simple as the task allows.

## 1. Identify the changes

Use the files, commits, or version range specified by the user and the current task context. If no range is specified, inspect the working tree in a Git repository that already has commits:

```bash
git status --short --untracked-files=all
git diff --stat HEAD
```

- Read relevant diffs and files as needed. Inspect untracked files separately and include only those related to the task.
- For a specified commit or version range, compare that range without mixing in unrelated working tree changes.
- If there are no relevant working tree changes, do not silently switch to the latest commit. The current task context or a specific documentation issue may still provide a basis for updates.
- Without Git or an initial commit, use the supplied change information and relevant files. Ask only when missing information affects accuracy; do not infer past behavior from current files alone.

## 2. Update the relevant documentation

Check whether changes affect features, usage, configuration, structure, or other existing explanations. Update the affected sections of the appropriate documents.

- Reuse existing documents, structure, terminology, and language. Leave accurate documentation unchanged.
- The language of this skill does not determine the output language. Follow the user's language requirements; otherwise, preserve each document's language. For a new document, follow the project's convention or the user's language if none exists.
- When the project maintains translations of an affected document, update the corresponding sections together unless the user limits the scope.
- Add a document only when an explanation is needed and no suitable place exists. Do not build an extra documentation system.
- Describe the actual resulting behavior. Check commands, paths, parameters, and defaults against relevant code or configuration. Do not invent reasons for changes or claim checks that were not performed.

## 3. Maintain the changelog

Record changes by default. Honor explicit limits such as "only update this README" or "only update the changelog."

- Use the project's existing changelog location and format. If none exists, create `CHANGELOG.md` at the project root with short entries grouped by the actual recording date.
- Explain what changed and its impact. Add the reason when known and useful, and relevant modules or paths when they help future searches. Internal refactoring, configuration changes, and documentation rule changes can also be worth recording.
- Summarize related changes together rather than listing every file. Do not require category labels, time of day, or version numbers.
- Check for existing coverage before adding an entry. Avoid duplicates and preserve history instead of rewriting old entries for formatting consistency.
- Wording or formatting edits that add no new facts usually do not need their own entry.

## 4. Check and report

Check that the documentation matches the changes, links and paths are valid, and changelog entries are clear and not duplicated. Keep unrelated edits out. Run relevant documentation checks required by the project; text edits do not require unrelated tests.

Briefly report which documents changed, what was recorded, and which change scope was used. Disclose unresolved information that affects the result. If no updates are needed, explain why.
