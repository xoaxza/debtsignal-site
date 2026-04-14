# Render deployment packet

## Identity
- task_id: debtsignal-site-2026-04-14
- repo_path: /home/abd/ai-agent-company/projects/debtsignal-site
- objective: Publish a public DebtSignal website with API info/docs for a future AI-agent-friendly SEC 8-K financing and covenant events API, then email the verified live link to team@scottyshelpers.org.
- deployment_authorization: approved

## Hosting policy
- standard_hosting_path: GitHub -> Render
- alternate_hosting_allowed: no
- fallback_policy_if_standard_path_fails: blocked_on_tooling_with_exact_evidence

## GitHub source requirements
- github_owner: xoaxza
- github_repo_name: debtsignal-site
- github_repo_visibility: public
- git_branch: main
- repo_url: https://github.com/xoaxza/debtsignal-site
- origin_remote_expected: https://github.com/xoaxza/debtsignal-site.git
- gh_auth_verified_in_current_runtime: yes
- gh_auth_evidence: `gh auth status` showed account `xoaxza` logged in with HTTPS protocol and token scopes including `repo`; `gh auth setup-git` completed before push.
- repo_push_completed: yes
- repo_push_evidence: `gh repo create xoaxza/debtsignal-site --public --source=. --remote=origin --push` succeeded and pushed branch `main`.

## Render target requirements
- deployment_provider: render
- owner_id: tea-d1upcpruibrs738nckqg
- workspace_name: Michael's workspace
- service_type: static_site
- service_name: debtsignal-site
- region: oregon
- auto_deploy_mode: yes

## Render build/runtime settings
For static sites:
- build_command: echo 'Static site ready'
- publish_path: .

For web services:
- runtime:
- build_command:
- start_command:
- health_check_path:
- required_env_vars:

## Verification plan
- local_verification_commands:
  - `python3 -m http.server 8002`
  - `python3 - <<'PY' ... json.loads(open('docs/openapi.json').read()) ... PY`
  - browser check at `http://127.0.0.1:8002/`
- live_verification_urls:
  - https://debtsignal-site.onrender.com
  - https://debtsignal-site.onrender.com/docs/openapi.json
  - https://debtsignal-site.onrender.com/docs/sample-event.json
- success_criteria:
  - live Render URL loads successfully
  - expected page content is present
  - machine-readable docs URLs return valid JSON
  - URL is safe to share in outbound email

## Handoff rules
- marketing_may_use_live_url_only_after_verification: yes
- email_recipient_list:
  - team@scottyshelpers.org
- email_should_be_blocked_if_live_url_missing: yes

## Failure handling
- if_gh_auth_fails_once: re-check in the current runtime
- if_render_check_fails_once: re-check in the current runtime
- if_repo_push_or_render_deploy_still_fails: stop and return blocked_on_tooling with exact command output
