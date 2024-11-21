
# Unity Google Play Games Plugin Setup Guide

## Package
- **Google Play Games Plugin**: `GooglePlayGamesPlugin-0.11.01.unitypackage`

## Overview
This guide provides instructions for integrating the Google Play Games Plugin into your Unity project. It also includes a troubleshooting section to resolve common issues encountered during setup.

## Installation
1. Download the `GooglePlayGamesPlugin-0.11.01.unitypackage` file from the official GitHub repository or relevant source.
2. Import the package into your Unity project:
   - Open Unity.
   - Go to `Assets → Import Package → Custom Package`.
   - Select `GooglePlayGamesPlugin-0.11.01.unitypackage` and import all files.

3. Follow the initial setup wizard for the plugin to configure your project.



<summary><strong>Troubleshooting</strong></summary>

### Problem: Could not find `com.google.games:gpgs-plugin-support:0.11.01`
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



### Problem: Failed to transform play-services-measurement-api-22.1.2.aar (com.google.android.gms:play-services-measurement-api:22.1.2) to match attributes {artifactType=android-dex, asm-transformed-variant=NONE,

<details>
**Symptoms**: Minimum SDK is too low

**Solution**:  
1. Project Settings > Player Minimum API Level:
   Change into API Level 28

</details>
