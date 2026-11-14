# NOVA BOOST — releases

Public update channel for **NOVA BOOST**, the CS2 performance tool for Windows.
The app is licensed and will not run without a valid PWF Auth key; nothing here bypasses that.

## How auto-update works
The app checks \`latest.json\` on this repo every 30 minutes (and on the About page).
If its \`version\` is newer than the running build, the app downloads the EXE at \`url\`,
verifies its SHA-256 against \`sha256\`, replaces itself and restarts. The download is
accepted only from github.com / githubusercontent.com and only if the hash matches.

## latest.json
\`\`\`json
{
  "version": "1.1.0",
  "notes": "What changed in this version.",
  "mandatory": false,
  "url": "https://github.com/LovableAdam/nova-boost-releases/releases/download/v1.1.0/NOVA_BOOST.exe",
  "sha256": "<64-hex SHA-256 of that exact EXE>"
}
\`\`\`

## Publishing an update
1. In the app source, raise \`kAppVersion\` in \`src/license/LicenseConfig.h\` (e.g. 1.1.0), build the protected EXE and sign it.
2. Get its hash:  PowerShell \`Get-FileHash .\\"NOVA BOOST.exe" -Algorithm SHA256\`  (lower-case it).
3. Here: **Releases → Draft a new release**, tag \`v1.1.0\`, upload the EXE **named \`NOVA_BOOST.exe\`**, publish.
4. Edit \`latest.json\`: set \`version\`, \`notes\`, the release \`url\` and the \`sha256\`.
5. Every running copy updates within 30 minutes. Set \`mandatory: true\` to require it before BOOST.

Keep \`version\` equal to the build you actually uploaded — the app refuses any EXE whose hash does not match.
