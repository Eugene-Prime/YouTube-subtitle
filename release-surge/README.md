# DualSubs YouTube local patch

This release uses the public upstream v1.5.11 YouTube bundles and public Universal bundles. Two paired changes close the Official recursion path: the Composite bundle deletes `tlang` and `subtype`, then marks its internal source-subtitle fetch; the YouTube TimedText request bundle detects that mark and does not add `tlang` or `subtype` again.

## LAN test

1. Disable every other DualSubs YouTube module.
2. Run `python3 -m http.server 8080 --directory .` in this directory.
3. Replace `REPLACE_LAN_IP` in `DualSubs.YouTube.Fixed.LAN.sgmodule` with this Mac's LAN IP.
4. Import that module into Surge, then select Auto translate → Chinese in YouTube.

For GitHub hosting, upload these files to a repository and replace `REPLACE_OWNER/REPLACE_REPO` in the non-LAN module.
