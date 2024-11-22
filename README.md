
# Unity Google Play Games, Firabase Crashlytic Plugin Setup Guide

## Package
- **Google Play Games Plugin**: `GooglePlayGamesPlugin-0.11.01.unitypackage`
- **External Dependency Manager**: `com.google.external-dependency-manager-1.2.183.tgz`
- **Firebase Core**: `com.google.firebase.app-12.4.1.tgz`
- **Firebase Crashlytic**: `com.google.firebase.crashlytics-12.4.1.tgz`

## Overview
This guide provides instructions for integrating the Google Play Games Plugin into your Unity project. It also includes a troubleshooting section to resolve common issues encountered during setup.

## Installation
1. Download the [GooglePlayGamesPlugin-0.11.01.unitypackage](https://github.com/playgameservices/play-games-plugin-for-unity/tree/master/current-build "GooglePlayGamesPlugin-0.11.01.unitypackage")` file from the official GitHub repository or relevant source.
2. Import the package into your Unity project:
   - Open Unity.
   - Go to `Assets → Import Package → Custom Package`.
   - Select `GooglePlayGamesPlugin-0.11.01.unitypackage` and import all files.
3. Remove ExternalDependencyManager folder <- this to prevent Redundant dependencies or sub-dependencies on both UPM and Custom Package which the EDM4U cannot resolve correctly.
4. Import Firebase packages using Unity Package Manager [Google APIs for Unity archive](https://developers.google.com/unity/archive)
 - External Dependency Manager (com.google.external-dependency-manager)
 - Firebase Core (com.google.firebase.app)
 - Firebase products used in your project. If you use Realtime Database or Cloud Storage, import Authentication (com.google.firebase.auth) first.

3. Follow the initial setup wizard for the plugin to configure your project.





## Troubleshooting

- Problem: NullReferenceException: Object reference not set to an instance of an object Google.JarResolver.Dependency.IsGreater

	**Symptoms**: Redundant dependencies or sub-dependencies on both UPM and Custom Package which the EDM4U cannot resolve correctly.

	**Solution**:  
	Apparently the issue was UPM registry
	-  Move to Min API 24 and target Highest possible API
	-  I removed the UPM package
	-  Removed the ExternalDependencyManager folder
	-  Installed EDM4U 1.2.183 from unity package found here
	-  Assets -> Refresh
		External Dependency Manager appeared but didn't showed the resolver
	-  Assets -> External Dependency Manager -> Version Handler -> Update 
		found an obsolete file, I applied what he proposed.
	-  Android resolver appear in External Dependency Manager
	-  Force resolve suceed instantly (good sign that it works)
	- Build succeed


- Problem: Could not find `com.google.games:gpgs-plugin-support:0.11.01`

	**Symptoms**: During Android dependency resolution, Unity reports that it cannot locate the required files.

	**Solution**:  
	- Open the file: `Assets/GooglePlayGames/com.google.play.games/Editor/GooglePlayGamesPluginDependencies.xml`
	- Locate the following line: `<repository>Packages/com.google.play.games/Editor/m2repository</repository>`
	- Replace it with:
`<repository>Assets/GooglePlayGames/com.google.play.games/Editor/m2repository</repository>`

	- Save and close the file.

	- In Unity, click:
	 `Assets → External Dependency Manager → Android Resolver → Force Resolve`

	- Raise your hands and thank the Almighty – you're done! 🎉




- Problem: `Failed to transform play-services-measurement-api-22.1.2.aar (com.google.android.gms:play-services-measurement-api:22.1.2) to match attributes {artifactType=android-dex, asm-transformed-variant=NONE,`

	**Symptoms**: Minimum SDK is too low

	**Solution**:  
	- Project Settings > Player Minimum API Level:
	   Change into API Level 28

