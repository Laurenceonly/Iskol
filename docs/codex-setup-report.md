# ISKOL Codex setup evidence

Activity date: October 12, 2026. Repository: https://github.com/Laurenceonly/iskol.

## Audit and scope

The audit found only local `main`, tracking `origin/main`, at `b1a2bc1`. Their local comparison was `0 0`; no remote fetch was used to claim remote freshness. There were 38 staged files and an unstaged deletion of the newly staged `CLAUDE.md`. The user's intentional deletion was subsequently preserved by removing that staged addition. Remaining unrelated application changes are excluded from the setup commit and are not discarded.

| Requirement | Initial state | Result |
| --- | --- | --- |
| Dedicated branch | Missing | `feature/ai-agent-setup` created from `main` |
| Agent instructions | Needs improvement | Existing `AGENTS.md` and `knowledge.md` expanded |
| Two custom skills | Missing | Two project skills created under `.agents/skills/` |
| Two provider skills | Complete in the local environment | Existing `frontend-design` and `impeccable` retained |

The user later authorized completing the remaining requirements together and committing/pushing only setup files. No application source was edited for this setup activity. No PR or merge is authorized by this activity.

## Requirement 1: feature branch

Executed commands included `git branch --show-current`, `git status`, `git branch -vv`, `git branch --all`, `git remote -v`, `git rev-list --left-right --count main...origin/main`, and `git switch -c feature/ai-agent-setup`.

Actual branch verification showed `feature/ai-agent-setup`, comparison `0 0` against `main`, `main commit unchanged: True`, and `working tree/index status unchanged: True`. Main remained at `b1a2bc1` after branch creation.

Report paragraph: Following a repository audit, a dedicated feature branch named `feature/ai-agent-setup` was created from `main`. Git verification confirmed that the feature branch was active and that the existing staged and unstaged work was preserved. The branch isolates the Codex setup activity while leaving the main branch unchanged.

## Requirement 2: project instructions

`AGENTS.md` preserves the generated Next.js guidance and adds an explicit instruction to consult `knowledge.md`, data and authorization rules, error handling, verification, scoped Git operations, and skill usage conditions. `knowledge.md` describes the verified stack, repository structure, student/admin workflows, observed Supabase contracts, environment variables, and unresolved backend details. It distinguishes baseline code from pending application changes excluded from this commit. `CLAUDE.md` and `CODEX.md` were not created.

Report paragraph: The existing agent instructions and project knowledge were reviewed and improved using verified repository contents. The updated instructions define Next.js and Supabase conventions, authorization boundaries, input validation, safe Git practices, and suitable verification commands. The knowledge document records core workflows and identifies database policies and RPC definitions that could not be confirmed locally.

## Requirement 3: custom skills

| Skill | Path | Purpose |
| --- | --- | --- |
| `iskol-cross-layer-feature` | `.agents/skills/iskol-cross-layer-feature/SKILL.md` | Coordinate routes/components, Supabase contracts, authorization, compatibility, and verification |
| `iskol-class-schedule-workflow` | `.agents/skills/iskol-class-schedule-workflow/SKILL.md` | Preserve recurring schedule linkage, weekday/time rules, permissions, errors, and consumers |

Each skill includes YAML `name` and `description`, focused usage conditions, actionable procedures, and verification steps. No scaffold placeholders or duplicate project skills were introduced. The current official Codex guide documents repository discovery under `.agents/skills/`; repository `.codex/skills/` support was not established for this runtime, so the documented path was used. Source: https://learn.chatgpt.com/docs/build-skills.

Validate with the bundled Skill Creator `scripts/quick_validate.py` against each directory. The current session's initial skill list is a startup snapshot; verify interactive discovery using the Codex skill selector (`$` or `/skills` in CLI/IDE) and reopen the session if necessary. Do not represent file validation as proof of a selector refresh or live workflow testing.

Actual validation on October 12, 2026 returned `Skill is valid!` with exit code 0 for both custom skill directories. The setup documentation diff passed whitespace checks. No application tests were added or run for this documentation/skill change.

Report paragraph, skill 1: The `iskol-cross-layer-feature` skill was created to guide coordinated feature development across ISKOL's Next.js interface and Supabase data layer. Its procedures address shared contracts, ownership, validation, compatibility, error handling, and verification while preserving existing application behavior.

Report paragraph, skill 2: The `iskol-class-schedule-workflow` skill was created for recurring class schedule maintenance. It records the subject relationship, weekday encoding, time-order rule, optional location handling, authorization dependencies, and required checks across subject details, the dashboard, and calendar.

## Requirement 4: provider skills

| Provider skill | Installed location | Verified source | Benefit |
| --- | --- | --- | --- |
| `frontend-design` | `C:/Users/MY_PC/.agents/skills/frontend-design/SKILL.md` | https://github.com/anthropics/skills/tree/main/skills/frontend-design | Responsive interface design and intentional typography/layout |
| `impeccable` | `C:/Users/MY_PC/.agents/skills/impeccable/SKILL.md` | https://github.com/pbakaus/impeccable | Frontend audits, accessibility, responsive behavior, and UI hardening |

Both manifests were read and both skills appear in this environment's available-skill catalog. The user-level `.agents/.skill-lock.json` records their source repositories. Frontend Design includes its referenced license; Impeccable includes its launcher and workflow references (installed metadata version `4.4.0`). No installation command was executed because suitable installations already existed. These user-level installations are not bundled into this repository or guaranteed on another computer.

Report paragraph: Two relevant provider skills were already installed and were retained after inspection. Frontend Design supports the application's interface design, while Impeccable supplies guidance for accessibility, responsive behavior, and interface hardening. Their manifests, source records, and supporting resources were inspected, avoiding duplicate installations.

## Final structure and screenshot evidence

```text
AGENTS.md
knowledge.md
.agents/skills/
  iskol-cross-layer-feature/SKILL.md
  iskol-class-schedule-workflow/SKILL.md
docs/codex-setup-report.md
```

Capture these genuine screens for submission:

1. Terminal: `git branch -vv`, `git branch --show-current`, and `git status`; show the feature branch and preserved application work.
2. Editor: `AGENTS.md` with the knowledge reference and authorization/verification sections; `knowledge.md` with workflows and known limitations.
3. Explorer and editor: both `.agents/skills/` folders and each skill's frontmatter/procedure. Include the validator output and the Codex skill selector after refresh if available.
4. Editor: both provider `SKILL.md` files and their source records in the user-level lock file.
5. Terminal/GitHub: `git show --stat HEAD`, the push output, and the feature branch page showing only the five setup files in the commit.

The filled academic PDF is a separate submission artifact, not application source. Personal information not provided by the student must be left visibly marked for completion rather than invented.

## Git integration

The authorized setup commit uses only the five paths shown above. Application changes remain pending. Push targets `origin feature/ai-agent-setup`; main is not pushed or merged. Verify using `git show --stat HEAD`, `git status`, and `git ls-remote --heads origin feature/ai-agent-setup`.

After review, an eventual PR should use `feature/ai-agent-setup` as the head and `main` as the base. Check the Files changed tab for the setup-only scope, review database/documentation limitations, and merge only after explicit authorization. No PR was created or merged as part of this setup.
