# Project memory

## Product intent & audience

- Poker application ("icy-poker-fix") with real-time table gameplay, chip management, and player accounts.
- Features include: sitting at tables, buying chips at a table, cashing out, referral codes, QR codes.
- Likely targets end-user players; includes signup flow with pre-login referral-code validation.

## Brand personality & voice

- Not yet inferred beyond functional/technical communication.

## Visual design & UX direction

- Not yet inferred from available context.

## Decisions, constraints & rationale

- **Backend:** Supabase (Postgres + Auth). Database has 10 tables, 19 functions, RLS enabled on all tables. Seeded settings and QR code rows exist.
- **Auth fix applied:** Two auto-generated Supabase connection files (browser client + server auth middleware) were updated to read the correct Bolt-provided environment variable names. These files may be regenerated, which would revert the fix.
- **Security posture:** Only `referral_code_exists` RPC is callable by anonymous users — intentionally left open because the signup page validates referral codes before login. All other server-only RPCs are restricted to the service role.
- **Quality gate:** App builds successfully, 33 automated tests pass, type check is clean. Linter reports many preexisting formatting errors across the codebase (not blocking runtime).
- **End-to-end gaps:** Sign-up, buying chips, and cashing out have not been tested against the live database (no players seeded yet).

## Open questions & assumptions

- Whether the env-variable fix should be made permanent in a non-auto-generated config to survive regeneration.
- Whether to clean up preexisting lint/formatting errors.
- Full sign-in and game flow needs live end-to-end testing once a player account is created.
- No visual design direction has been provided or inferred yet.