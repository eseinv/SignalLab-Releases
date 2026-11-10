# Portable and managed deployment

SignalLab 0.9 Preview targets Windows 10/11 x64 with the bundled .NET 10/WPF runtime. Use a Windows version supported by the site's Microsoft servicing policy. The supplied tests establish behavior on the recorded build host, not every Windows/firmware combination. Stable release qualification remains separate.

1. Download the complete portable ZIP from the official releases page. Verify its SHA-256 and the updater's authenticated manifest/offline package when distributing it. Extract the whole folder, including `current`, the launcher and recovery helper; do not copy just SignalLab.exe.
2. Choose a site-approved executable location. A standard user can run a self-contained extraction without installing .NET or granting SignalLab administrator rights. App binaries do not need to share a writable directory with data. In-place self-update requires write access to its install root; for administrator-owned/read-only deployments, have the administrator replace the complete qualified package instead of weakening ACLs.
3. User settings, update cache, indexes and support state use `%LOCALAPPDATA%\SignalLab`. Permanent captures default to `Documents\SignalLab\DataRecords\yyMMdd`, or the explicit root selected in Configure → Data storage. Ensure the user's storage/backup roots have sufficient permissions/space. Profiles must not share writable ownership state across different users.
4. Start with simulation; confirm storage, stop/start, pause/Follow live and historical reopen. Importing a workspace creates a new stopped project, remaps recording storage and resets backup paths/counters. Review connection routes before explicitly starting it. A workspace export can include explicitly selected capture copies/references; unresolved references require manual file selection. Sanitized review copies contain no operational settings and cannot be imported.
5. The optional Preview publisher certificate is separate from update authenticity. Verify its documented fingerprint before a site administrator decides whether to trust it. No certificate installation, global proxy change or trust-store change is performed by the test suite or ordinary app startup.

## Offline and managed updates

Help → Check for updates has persistent Offline mode. Online checks/downloads are disabled; importing a `.slupdate` still verifies its pinned release signature, policy and package hash. A disconnected/blocked/proxy-error check must never be interpreted as “up to date.” Recording continues unless the user accepts an update, at which point the app finalizes captures and disconnects before handing off; qualified restart/rollback resumes the prior intent.

Administrators can place `update-policy.json` under `%PROGRAMDATA%\SignalLab`, with administrators/system as writers and ordinary users as readers:

```json
{"OnlineChecks":false,"Channel":"preview","ApprovedVersion":"0.9.0-preview.30"}
```

Omit `ApprovedVersion` for no exact-version pin. Unknown/invalid policy fields and unreadable/malformed policy fail closed. This policy cannot replace the pinned signing key or bypass integrity checks. Deploy an authenticated offline bundle for the approved version. Clearing Offline mode cannot override an administrator's disabled-online policy.

The online client uses Windows/.NET's configured proxy behavior. Permit outbound HTTPS to the official GitHub release/feed locations and approved `githubusercontent.com` download redirects; no inbound firewall rule is required. Configure a site proxy through the site's supported Windows process/user policy. A `407` response means proxy authentication is required; involve the administrator. SignalLab does not collect proxy passwords or disable TLS verification. An offline update is the supported alternative when online access cannot be approved.

## Runtime and artifact inventory

`current/SBOM.cdx.json` is a CycloneDX 1.6 inventory generated after packing/signing, including NuGet dependencies, .NET/WPF framework versions and hashes of actual managed/native/support files. The SBOM omits its own hash; the signed manifest binds the complete downloadable archive. Qualification verifies every inventoried file and rejects missing runtime/SQLite components. Runtime fixes require a newly built and qualified SignalLab package, even if system .NET has been updated.

## Acceptance evidence and limits

This batch verifies an isolated app-data deployment using an actual non-administrator token, absent system-runtime environment override in the self-contained release gate, persisted Offline policy and real loopback CONNECT/TLS traffic with a test-only certificate. Successful proxy transport retains signed-metadata verification; `407` is an error; Offline mode produces no CONNECT. No system proxy/certificate settings are changed.

Before site rollout, independently validate a clean customer account/PC, executable restrictions, actual corporate proxy/TLS policy, physical 16 GB workload, real PLC permissions/firmware, interruption/recovery and backups. Logical viewport tests do not establish physical mixed-DPI or OS high-contrast acceptance. Keep approved packages and rollback data until the new version passes site acceptance. Preview remains an engineering tool, not a safety or unattended service product.
