## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/90

**Issue title:** Add integration tests for authentication edge cases

**Tier:** [ ] Tier 1  [x] Tier 2  [ ] Tier 3

**Problem summary:**
The auth middleware only has tests for the happy path — a valid token. There are no tests covering what happens when someone sends an expired token, a malformed one, a token signed with the wrong secret, or no Authorization header at all. These are exactly the cases that matter for security, since real attackers won't be sending valid tokens. The fix is adding integration tests to the existing test_auth_middleware.py file that cover each of these four edge cases and confirm the middleware rejects them correctly.

**Branch name:** test/90-auth-middleware-edge-cases

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [ ] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/R1sh1-11/pathreview/commit/681dca4

**Reproduction summary:**
Confirmed `tests/integration/test_auth_middleware.py` does not exist in the repo — the issue is a gap in test coverage, not a broken behavior. Added a new test file with 4 failing/pending integration tests that document exactly what's missing: expired token, malformed token, missing header, and wrong-secret token all need to return 401.

**PLAN.md link:** [https://github.com/R1sh1-11/pathreview/blob/test/90-auth-middleware-edge-cases/PLAN.md](https://github.com/R1sh1-11/pathreview/blob/test/90-auth-middleware-edge-cases/PLAN.md)

**Blockers or open questions:**
The test client may trigger the app lifespan and require Docker/Postgres to be running during test execution. Need to confirm whether tests need a live DB or if the DB dependency can be mocked out for pure auth middleware testing.

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
All 4 sub-tasks from PLAN.md are done. The test file covers expired tokens, malformed tokens, missing Authorization header, and wrong-secret tokens, and all 4 pass locally. Also caught and fixed a bug in my own plan, PLAN.md originally pointed at `GET /profiles`, which does not exist, so I switched the tests to hit `GET /profiles/{profile_id}` instead since it uses the same auth dependency.

**Next steps:**
Get peer or mentor feedback on the draft PR in Slack, then address anything that comes up before marking it ready for review.

**Blockers:**
None right now.
