# Testing and CI
Owner requirement: automated unit through system testing, pytest for Python, Catch2/CTest for custom C++, cargo test/proptest for Rust if justified, XCTest/Swift Testing for iOS. No language introduced solely for testing.

## Layers
Unit and property tests (pytest, pytest-asyncio, Hypothesis); component lifecycle and adapter contract suites; integration with real temporary SQLite and mock external services; container system tests via public API; security, recovery and hardware acceptance. Real model tests are separate from deterministic mock tests. No personal data or paid APIs in fixtures.

## State machines
Test transition tables, invalid events, idempotency, cancellation/completion races, deadlines, shutdown, overload, process death, recovery and resource ownership. Distinguish cancellation requested from confirmed termination; terminal outcomes are immutable. Use injected clocks, deterministic synchronization, bounded timeouts and seeded/reproducible generated cases, not arbitrary sleeps. Verify committed state and independent reminders survive inference failure. Runtime state reconstructed after restart.

## CI stages
PR: lint/type checks, unit/property tests, component/contract tests, integration tests, CPU container build and system tests. Run on main too. Fail on missing tests once implementation begins; do not count empty suites as passing. Publish JUnit and coverage artifacts. Initially target 85% branch coverage for Python domain and lifecycle code, with explicit review of exceptions; coverage is not proof of correctness. Native C++ jobs when introduced: CMake/CTest Catch2, sanitizers where supported. Rust jobs when introduced: fmt, clippy, cargo test. iOS jobs on macOS when app exists. ARM64 image build and smoke test before release; Jetson GPU acceptance on dedicated trusted hardware, never run untrusted public PRs on household hardware. Model quality and latency suites opt-in/nightly when resources exist. No hardware performance claims from CPU CI.

## System scenarios
Shopping contextual update and undo, receipt duplicate and injection, reminder across restart and inference failure, two-user isolation, revoked device, offline core, invalid tool calls, printer ambiguous outcome, backup/restore. Use synthetic data. Test API compatibility and migrations from previous supported version. Fault injection and bounded concurrency tests. Track p50/p95 latency and peak memory on fixed hardware; set regression thresholds after baseline.

## Governance
Required checks and owner review before merge; repository branch protection configured by owner if available. No bypass, no unapproved architecture changes. Pin dependencies and action revisions before production use; least privilege CI token, no secrets for untrusted PRs. Initial documentation-only workflow must be labeled as such; full gates become mandatory with implementation. Test failures block merge. Flaky tests are tracked and fixed, not silently retried into green.
