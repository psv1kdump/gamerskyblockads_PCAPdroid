# Gamersky Android AdGuard Filter (Experimental)

A conservative, app-scoped AdGuard filter draft for the Gamersky (游民星空) Android app, based on one PCAPdroid capture supplied by a user on 2026-10-26.

## Status

**Experimental — not yet validated on-device.** The candidate endpoints below were observed in the capture and their path names suggest ad-related functions. A single capture does not prove that blocking them will remove the corresponding ads without side effects.

## Candidate endpoints

- `router10.gamersky.com/@/adSystem/ad/getAppPopupAd` — observed POST endpoint; path name suggests a popup-ad API.
- `router10.gamersky.com/@/adSystem/ad/getAdAtLaunchView` — observed POST endpoint; path name suggests a launch-view ad API.
- `router10.gamersky.com/@/adSystem/ad/getAndroidTouTiaoWangMengAd` — observed GET endpoint; path name suggests a Toutiao/Wangmeng ad API.

Rules are scoped to the observed app package `com.gamersky` using AdGuard's `$app` modifier. If your AdGuard version does not support or apply this modifier, check the filtering log before assuming the rules are active.

## Install

1. Open AdGuard for Android and find **Settings → Content blocking → Custom filters** (menu wording may vary by version).
2. Add this raw filter URL: `https://raw.githubusercontent.com/psv1kdump/gamerskyblockads_PCAPdroid/main/gamersky-adguard.txt`
3. Update the filter and verify it is enabled.
4. Force-stop and reopen Gamersky. Test startup, homepage/feed, article details, images, comments, login, and other normal functions.
5. Check AdGuard's filtering log to confirm whether any candidate rules match.

## Test and report

- If ads remain, capture a new PCAPdroid trace focused on that ad scenario and share the relevant connection details.
- If any app feature breaks, disable the filter and report the affected screen plus the matching AdGuard log entry.
- Treat each rule as a candidate until a before/after test confirms its effect.

## Limitations

- Only one capture has been reviewed; no on-device before/after validation has been performed.
- Encrypted HTTPS payloads may hide response bodies and other details.
- Endpoint names are suggestive, not conclusive proof of advertising behavior.
- Ads delivered by shared content APIs, embedded content, or other domains may not be removed by these rules.
- Domain/path blocking cannot selectively rewrite arbitrary encrypted response bodies.

## Privacy

Do not commit raw PCAP files to this repository. Captures may contain device identifiers, account identifiers, URLs, tokens, and other sensitive metadata.
