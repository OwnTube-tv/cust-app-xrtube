# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

**XR Tube** is a branded app repository for OwnTube.tv, containing ONLY branding configuration and CI/CD orchestration. This is one of multiple production branded apps (see others: cust-app-blender, cust-app-basspistol, cust-app-pitube).

**⚠️ For technical documentation, architecture, and development guidance, see:**
- **[Upstream CLAUDE.md](https://github.com/OwnTube-tv/web-client/blob/main/CLAUDE.md)** - Complete documentation
- **Upstream repo:** [OwnTube-tv/web-client](https://github.com/OwnTube-tv/web-client)
- **Customization docs:** [docs/customizations.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/customizations.md)
- **Pipeline setup:** [docs/pipeline.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md)

All source code, tests, and development tooling live in the upstream repository. This repo uses GitHub Actions workflow reuse to delegate builds to upstream.

## XR Tube Brand Identity

**App Name:** XR Tube
**Description:** Information videos by Extinction Rebellion
**Primary Backend:** tube.rebellion.global
**Package IDs:** com.owntubetv.xrtube (iOS & Android)

**Legal Entity:** OwnTube Nordic AB
**Contact:** legal@owntube.tv, hello@owntube.tv

**Deployments:**
- Web: [cust-app-xrtube.owntube.tv](https://cust-app-xrtube.owntube.tv)
- iOS/tvOS: [TestFlight beta](https://testflight.apple.com/join/EzReSmsz)
- Android/TV: [Google Play](https://play.google.com/store/apps/details?id=com.owntubetv.xrtube)

**Branding:**
- Primary color: `#65A454` (green)
- Splash background: `#65A454`
- Theme: `#FFFFFF` (white)
- Analytics: PostHog enabled (`phc_gd5UCB2Q6EQZz75oiAAc7Gn1PVErmJnIbebEtvMkPMf`)
- Git details: Hidden (`EXPO_PUBLIC_HIDE_GIT_DETAILS=1`)

## Repository Structure

```
.customizations              # XR Tube brand configuration
.github/workflows/           # CI/CD orchestration (delegates to upstream)
assets/                      # XR Tube branding images (14 files)
README.md                    # Customization guide (see this for asset dimensions)
```

## Common Tasks

### Update Branding Configuration

```bash
# 1. Edit .customizations file
vi .customizations

# 2. Replace assets in ./assets/ (maintain exact dimensions - see README.md)
# 3. Commit and push changes
# 4. Manually trigger: GitHub Actions → "Build mobile artifacts..." → Run workflow
```

### Deploy New Release

```bash
# Navigate to: GitHub Actions → "Build mobile artifacts & deploy..." → Run workflow
```

**Workflow options:**
- `upload_ios_to_testflight` - Upload to iOS TestFlight
- `upload_tvos_to_testflight` - Upload to tvOS TestFlight
- `google_play_track` - Upload to Google Play (none/internal/alpha/beta/production)
- `google_play_upload_tv` - Include Android TV upload

**Note:** Builds are MANUAL only (push-button releases). No automatic deployment on commit.

### Sync with Upstream Template

When upstream [OwnTube-tv/web-client](https://github.com/OwnTube-tv/web-client) updates workflows:

```bash
# 1. Review upstream changes
# 2. Update .github/workflows/ if workflow signatures changed
# 3. Update .customizations if new variables available
# 4. Test build before deploying to production
```

### Test Changes

**No local testing available.** To test branded app changes:

1. Trigger build via GitHub Actions (workflow_dispatch)
2. Download artifacts or use distribution platforms:
   - **iOS/tvOS:** TestFlight beta
   - **Android:** Google Play Internal Test track
   - **Web:** GitHub Pages deployment

### Develop New Features or Experiment with Customizations

To develop features or test customizations that require changes to upstream code:

1. **Fork** [OwnTube-tv/web-client](https://github.com/OwnTube-tv/web-client) to your own repository
2. Use this branded app repo with your fork by updating workflows:
   - Change `uses: OwnTube-tv/web-client/.github/workflows/...@main`
   - To: `uses: YOUR_USERNAME/web-client/.github/workflows/...@YOUR_BRANCH`
3. Make changes in your forked web-client repo
4. Test by triggering this branded app's workflow (which now uses your fork)
5. Once stable, contribute changes back to upstream via PR

See [upstream CLAUDE.md](https://github.com/OwnTube-tv/web-client/blob/main/CLAUDE.md) for local development commands in your forked repo.

### Initial Google Play Setup

First-time Google Play upload (generates initial AAB bundle):

```bash
# GitHub Actions → "Google Play initial bundle" → Run workflow
```

## Key Configuration Variables

See `.customizations` file for current XR Tube configuration. Complete variable reference in [upstream docs/customizations.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/customizations.md).

**Critical variables:**
- `EXPO_PUBLIC_APP_NAME` - App display name
- `EXPO_PUBLIC_PRIMARY_BACKEND` - PeerTube instance hostname
- `EXPO_PUBLIC_ICON` - Main app icon (512x512)
- `EXPO_PUBLIC_SPLASH_IMAGE` - Splash screen (1152x1152)
- `EXPO_PUBLIC_POSTHOG_API_KEY` - Analytics key (or `null` to disable)

**Asset path convention:** Use `../customizations/assets/[filename]` when referencing local files.

## Secrets & Environments

All secrets stored in `owntube` GitHub environment. Required for builds:

**Android:** Keystore, signing credentials, Google Play service account
**iOS/tvOS:** Certificates, provisioning profiles, App Store Connect API keys

See [upstream docs/pipeline.md](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md) for complete setup instructions.

## Important Notes

- **No local builds** - All builds via GitHub Actions in upstream repo
- **No source code** - Only configuration and assets here
- **No tests** - Testing in upstream repository
- **Manual deployments** - No CI/CD automation on push
- **Asset dimensions matter** - See README.md for exact sizes required

## Related Repositories

- **Upstream:** [OwnTube-tv/web-client](https://github.com/OwnTube-tv/web-client) - Main codebase
- **Template:** [OwnTube-tv/cust-app-template](https://github.com/OwnTube-tv/cust-app-template) - New app template
- **Other branded apps:** cust-app-blender, cust-app-basspistol, cust-app-pitube
- **Dev/test fork:** [mykhailodanilenko/web-client](https://github.com/mykhailodanilenko/web-client) - "Misha Tube"
