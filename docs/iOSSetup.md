## iOS Setup

* Install Plugin.FacebookClient package into your iOS project.


### AppDelegate.cs


On **FinishedLaunching** just before **return base.FinishedLaunching(app, options)**:

```cs
FacebookClientManager.Initialize(app,options);
```

Override **OnActivated(UIApplication uiApplication)**:
```cs
FacebookClientManager.OnActivated();
```

Override OpenUrl methods

```cs
  public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
  {
      return FacebookClientManager.OpenUrl(app, url, options);
  }

  public override bool OpenUrl(UIApplication application, NSUrl url, string sourceApplication, NSObject annotation)
  {
      return FacebookClientManager.OpenUrl(application, url, sourceApplication, annotation);        
  }

```

### Info.plist

Add facebook bundle url types:


```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLName</key>
    <string>fb</string>
    <key>CFBundleURLSchemes</key>
    <array>
       <string>fbxxxxxxxxxxxxx</string>
    </array>
  </dict>
</array>
<key>FacebookAppID</key>
<string>xxxxxxxxxxxxx</string>
<key>FacebookDisplayName</key>
<string>[Facebook app name]</string>
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>fbapi</string>
  <string>fb-messenger-share-api</string>
  <string>fbauth2</string>
  <string>fbshareextension</string>
</array>
```

**Note: Replace xxxxxxxxxxxxx with your facebook app id**

If your app needs access to the gallery because will be posting photos, remember to add the photo library permission.

```xml
<key>NSPhotoLibraryUsageDescription</key>
<string>{human-readable reason for photo access}</string>
```


### Entitlement.plist

On your **Entitlement.plist** add:


```xml
  <key>keychain-access-groups</key>
  <array>
    <string>{your-apple-app-id-prefix}.{your-apple-app-id-bundle-identifier}</string>
  </array>
```

<= Back to [Table of Contents](../README.md)
