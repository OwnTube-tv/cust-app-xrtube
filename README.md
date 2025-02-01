# OwnTube Branded App Template

A template repository for creating a customized branded OwnTube instance. This repository provides the structure and configuration required to set up a fully branded app for OwnTube.

## Overview

This template allows you to easily:

- Customize the app name, icon, and splash screen.
- Restrict the app to a specific OwnTube backend.
- Generate configurations for both web and mobile platforms.

---

## How to Use

Follow the steps below to customize and deploy your branded OwnTube instance.

### 1. Create a `.customizations` File

In the root of the repository, create a `.customizations` file. This file will contain your app-specific customizations. Use it to define the following variables:

### 2. Restrict the App to a Primary Backend

Add the following line to your `.customizations` file:
```bash
EXPO_PUBLIC_PRIMARY_BACKEND=<your_instance_hostname>
```
This restricts the app to the specified hostname and disables instance selection in the web app. Note that users can still bypass this restriction by entering a different hostname in the URL parameters.

### 3. Configure App Customizations

#### All Platforms
Define the following variables for all platforms:

- **App Name:**
  ```bash
  EXPO_PUBLIC_APP_NAME=<your_app_name>
  ```
  The name of the app displayed throughout.

- **App Slug:**
  ```bash
  EXPO_PUBLIC_APP_SLUG=<your_app_slug>
  ```
  A unique identifier for your app.

- **App Icon:**
  ```bash
  EXPO_PUBLIC_ICON=<your_icon_url>
  ```
  The global icon used in the app. Size: arbitrary but looks best if 512x512 is reused here.

#### Web Platform
Define the following variables for the web platform:

- **Favicon:**
  ```bash
  EXPO_PUBLIC_FAVICON_URL=<your_favicon_url>
  ```
  The URL of the favicon for your site. Size: 32x32.

- **Base URL:**
  ```bash
  EXPO_PUBLIC_BASE_URL=<your_repo_name>
  ```
  The base URL used by Expo when deploying to GitHub Pages or similar services.

#### Mobile Platform
Define the following variables for the mobile platform:

- **Splash Screen Background Color:**
  ```bash
  EXPO_PUBLIC_SPLASH_BG_COLOR=<your_splash_bg_color>
  ```
  The background color for the splash screen.

- **Splash Screen Image:**
  ```bash
  EXPO_PUBLIC_SPLASH_IMAGE=<your_splash_image_path>
  ```
  The splash screen image file. Size: 1152x1152, transparent background.

- **Android TV:**
  ```bash
  EXPO_PUBLIC_ANDROID_TV_BANNER=<your_android_tv_banner_path>
  ```
  The Android TV banner image file. Size: 320x180.

- **Apple TV Icons:**
  ```bash
  EXPO_PUBLIC_APPLE_TV_ICON=<your_apple_tv_icon_path>
  EXPO_PUBLIC_APPLE_TV_ICON_SMALL=<your_apple_tv_icon_small_path>
  EXPO_PUBLIC_APPLE_TV_ICON_SMALL_2X=<your_apple_tv_icon_small_2x_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF=<your_apple_tv_top_shelf_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF_2X=<your_apple_tv_top_shelf_2x_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE=<your_apple_tv_top_shelf_wide_path>
  EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE_2X=<your_apple_tv_top_shelf_wide_2x_path>
  ```
  Apple TV-specific icons and top shelf images. Sizes:
  -  icon: 1280x768
  -  iconSmall: 400x240
  -  iconSmall2x: 800x480
  -  topShelf: 1920x720
  -  topShelf2x: 3840x1440
  -  topShelfWide: 2320x720
  -  topShelfWide2x: 4640x1440

---

## Example `.customizations` File

Here is an example `.customizations` file for reference:

```bash
EXPO_PUBLIC_PRIMARY_BACKEND=<your_instance_hostname>
EXPO_PUBLIC_APP_NAME=<your_app_name>
EXPO_PUBLIC_APP_SLUG=<your_app_slug>
EXPO_PUBLIC_ICON=<your_icon_url>
EXPO_PUBLIC_FAVICON_URL=<your_favicon_url>
EXPO_PUBLIC_BASE_URL=<your_repo_name>
EXPO_PUBLIC_SPLASH_BG_COLOR=<your_splash_bg_color>
EXPO_PUBLIC_SPLASH_IMAGE=<your_splash_image_path>
EXPO_PUBLIC_ICON=<your_app_icon_path>
EXPO_PUBLIC_HIDE_VIDEO_SITE_LINKS=<1 or 0>
EXPO_PUBLIC_APPLE_TV_ICON=<your_apple_tv_icon_path>
EXPO_PUBLIC_ANDROID_TV_BANNER=<your_android_tv_banner_path>
EXPO_PUBLIC_APPLE_TV_ICON_SMALL=<your_apple_tv_icon_small_path>
EXPO_PUBLIC_APPLE_TV_ICON_SMALL_2X=<your_apple_tv_icon_small_2x_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF=<your_apple_tv_top_shelf_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF_2X=<your_apple_tv_top_shelf_2x_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE=<your_apple_tv_top_shelf_wide_path>
EXPO_PUBLIC_APPLE_TV_TOP_SHELF_WIDE_2X=<your_apple_tv_top_shelf_wide_2x_path>
```

---

## Notes

- **Image and Custom File Paths:**
  If you want to include custom images or other files directly in this repository, place them in a `/customizations` folder. When referencing these files in the `.customizations` file, use paths starting with `../customizations/`. This is the path structure that the build process expects.

  For example:
  ```bash
  EXPO_PUBLIC_SPLASH_IMAGE=../customizations/assets/splashScreen.png
  EXPO_PUBLIC_ICON=../customizations/assets/icon.png
  ```
- **Code Signing for Apple & TestFlight:**
  Setting up code signing and TestFlight for Apple devices requires additional configuration. Refer to the [OwnTube Documentation](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md) for detailed instructions on configuring code signing and deploying your app to TestFlight.
- **Code Signing for Android & Google Play:**
  Refer to the [OwnTube Documentation](https://github.com/OwnTube-tv/web-client/blob/main/docs/pipeline.md) for detailed instructions on how to configure delivery to Google Play.
- Ensure all referenced files (e.g., icons and splash images) exist in the specified paths.
- Double-check the configurations before deploying to avoid runtime errors.

