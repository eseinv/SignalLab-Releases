# Security policy

Security owner and release maintainer: **Ievgen Sein**.

Report suspected vulnerabilities privately using [Report a vulnerability](https://github.com/eseinv/SignalLab-Releases/security/advisories/new) in the official downloads repository. Do not put plant addresses, production recordings, credentials or exploitable details in public issues. Include the app version, Windows version, minimal reproduction and expected versus observed behavior. Use synthetic data; ask before sending a real capture. Reports are reviewed by the owner, who coordinates reproduction, remediation and disclosure. No response-time guarantee or unattended monitoring service is implied.

The current Preview receives security fixes through a qualified newer Preview; older builds are not separate maintenance branches. Supported Windows deployments and limitations are in [DEPLOYMENT.md](docs/DEPLOYMENT.md). Stable support commitments will be stated when a stable release is published.

Every release checks direct/transitive packages, records the bundled runtime and native files in `current/SBOM.cdx.json`, and verifies its inventory against the actual downloadable archives. The owner reviews dependency/runtime advisories before publication and when a relevant vulnerability is reported, updates affected dependencies/runtime, reruns the release gate and publishes a verified update. A self-contained app receives runtime fixes by updating SignalLab; updating a separately installed .NET runtime does not service its bundled runtime.

The updater verifies its pinned release signature and package hash. The optional self-signed Preview Windows certificate is a separate publisher-trust mechanism. Never disable authenticity checks, accept an unknown key, or install a certificate obtained through an untrusted channel to work around an update failure.

See [the threat model and data policy](docs/SECURITY-BOUNDARIES.md). This policy does not claim certification, PLC safety functions, authenticated plant transport, tamper-evident recordings or protection against an administrator/compromised Windows account.
