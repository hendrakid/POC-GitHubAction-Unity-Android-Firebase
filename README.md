
# Unity Google Play Games, Firabase Crashlytic Plugin Setup Guide

## Package
- **Google Play Games Plugin**: `GooglePlayGamesPlugin-0.11.01.unitypackage`
- **Google Play Games Plugin**: `com.google.external-dependency-manager-1.2.183.tgz`
- **Google Play Games Plugin**: `com.google.firebase.app-12.4.1.tgz`
- **Google Play Games Plugin**: `com.google.firebase.crashlytics-12.4.1.tgz`
- **Google Play Games Plugin**: `GooglePlayGamesPlugin-0.11.01.unitypackage`

## Overview
This guide provides instructions for integrating the Google Play Games Plugin into your Unity project. It also includes a troubleshooting section to resolve common issues encountered during setup.

## Installation
1. Download the `GooglePlayGamesPlugin-0.11.01.unitypackage` file from the official GitHub repository or relevant source.
2. Import the package into your Unity project:
   - Open Unity.
   - Go to `Assets → Import Package → Custom Package`.
   - Select `GooglePlayGamesPlugin-0.11.01.unitypackage` and import all files.
3. Remove ExternalDependencyManager folder <- this to prevent Redundant dependencies or sub-dependencies on both UPM and Custom Package which the EDM4U cannot resolve correctly.
4. Import Firebase packages using Unity Package Manager [Google APIs for Unity archive]([https://awesomeopensource.com/project/elangosundar/awesome-README-templates](https://developers.google.com/unity/archive))
 - External Dependency Manager (com.google.external-dependency-manager)
 - Firebase Core (com.google.firebase.app)
 - Firebase products used in your project. If you use Realtime Database or Cloud Storage, import Authentication (com.google.firebase.auth) first.

3. Follow the initial setup wizard for the plugin to configure your project.



<summary><strong>Troubleshooting</strong></summary>


- ### Problem: NullReferenceException: Object reference not set to an instance of an object Google.JarResolver.Dependency.IsGreater,
<details>
**Symptoms**: Redundant dependencies or sub-dependencies on both UPM and Custom Package which the EDM4U cannot resolve correctly.

**Solution**:  
Apparently the issue was UPM registry

1. Move to Min API 24 and target Highest possible API
2. I removed the UPM package
3. Removed the ExternalDependencyManager folder
4. Installed EDM4U 1.2.183 from unity package found here
5. Assets -> Refresh
   External Dependency Manager appeared but didn't showed the resolver
6. Assets -> External Dependency Manager -> Version Handler -> Update
   He found an obsolete file, I applied what he proposed.
7. Android resolver appear in External Dependency Manager
8. Force resolve suceed instantly (good sign that it works)
Build succeed
   
</details>


- ### Problem: Could not find `com.google.games:gpgs-plugin-support:0.11.01`
<details>
**Symptoms**: During Android dependency resolution, Unity reports that it cannot locate the required files.

**Solution**:  
1. Open the file:  
   `Assets/GooglePlayGames/com.google.play.games/Editor/GooglePlayGamesPluginDependencies.xml`

2. Locate the following line:  
   <repository>Packages/com.google.play.games/Editor/m2repository</repository>

3. Replace it with:
   <repository>Assets/GooglePlayGames/com.google.play.games/Editor/m2repository</repository>

4. Save and close the file.

5. In Unity, click:
Assets → External Dependency Manager → Android Resolver → Force Resolve

6. Raise your hands and thank the Almighty – you're done! 🎉

</details>



- ### Problem: Failed to transform play-services-measurement-api-22.1.2.aar (com.google.android.gms:play-services-measurement-api:22.1.2) to match attributes {artifactType=android-dex, asm-transformed-variant=NONE,

<details>
**Symptoms**: Minimum SDK is too low

**Solution**:  
1. Project Settings > Player Minimum API Level:
   Change into API Level 28

</details>
