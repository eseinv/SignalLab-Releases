# SignalLab downloads

Official Windows x64 portable downloads by **Ievgen Sein, creator and project owner**.
This repository contains compiled releases, public verification material and update feeds.
SignalLab's source code is maintained separately and is not published here.

Open [Releases](https://github.com/eseinv/SignalLab-Releases/releases) and download the **Portable.zip** asset.
Extract the complete folder to a writable location and run its top-level **SignalLab.exe**.
The .NET desktop runtime is included; no .NET installation is needed.

Use **Help → Check for updates** inside SignalLab for signature-verified updates.
The Preview channel receives current development releases; Stable receives designated stable releases.
For offline PCs, transfer the release's `.slupdate` file and choose **Open offline update** in that window.
Downloads do not interrupt recording. Choosing **Update** finalizes active recordings and closes
connections, then installs and restarts. Recording resumes if it was running before installation.

Projects default to `Documents/SignalLab/Projects`; recordings default to
`Documents/SignalLab/DataRecords/yymmdd`. Settings and supporting files use `%LOCALAPPDATA%/SignalLab`.
Custom recording paths remain supported.

Update manifests are ECDSA P-256 signed; the application pins the public verification key and checks
the package's SHA-256 digest and size. The public key here is for transparency; the app does not
replace its trusted key from this repository. This update signature is separate from Windows
Authenticode publisher signing. Previews may include an optional self-signed publisher certificate
in the ZIP. Verify its SHA-256 against the release notes and follow the included portable README
if you choose to trust the publisher on your Windows account. SmartScreen may still show a
reputation prompt.

Automatic rollback retains a verified previous version. The new app must open within 90 seconds and
remain responsive for a 5-minute trial. A crash or a UI heartbeat missing for 25 seconds restores the
previous version; normal closing pauses the trial until the next launch. PLC disconnection alone does
not count as an application failure. Recovery restores UI/storage settings and resumes recording if it
was previously running. Existing recording files are retained; a forced termination may lose in-flight samples.
The latest previous version remains available after verification; older successful snapshots are pruned.

Keep a previous portable ZIP for recovery: close the app, extract it into a new folder and launch it.
Settings backups are kept under `%LOCALAPPDATA%/SignalLab/updates/backups`; updates do not delete recordings.

Public access permits downloading official releases. It does not grant repository write access or
permission to redistribute, modify, sublicense or sell SignalLab. See [LICENSE.txt](LICENSE.txt).
Third-party components retain their respective licenses.
