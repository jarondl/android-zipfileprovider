android-zipfileprovider
=======================

An android library that allows direct read access to files stored
in a compressed zip, via a content provider.
It uses ZipResourceFile from Google Play's
[APK Expansion Zip Library][APKEZ], and actually replaces APEZProvider
from the same library. Contrary to APEZProvider, this library allows access
to compressed files, and works with arbitrary zip files (not just apk expansion files).

How to use
------------

To use the library, you need to extend the class by implementing two methods:

    package com.example.MyPackage;

    import net.jarondl.zipfileprovider.ZipFileProvider;


    public class MyNewProvider extends ZipFileProvider {
        @Override
        public String getAuthority(){
            return "your_authority";
        }
        @Override
        public String ZipPath(){
            return the_zip_file_path.zip;
        }

    }

And you need to add the authority to your manifest:

        <provider android:authorities="com.example.MyPackage"
         android:name=".MyPackage"
         android:exported="true"></provider>
         
Then any app that can access content providers can read your files using a
 `content://" + AUTHORITY + FILE_PATH` uri.
 
 
Implementation exmple
------------
The motivation for this library was OxygenGuide.
You can see the complete implementation on this [branch][og-branch],
specifically notice the [manifest][og-manifest] and [OxygenProvider.java][og-provider]

[APKEZ]:  http://developer.android.com/google/play/expansion-files.html#ZipLib
[og-branch]: https://github.com/jarondl/OxygenGuide-Android/tree/new_zip_handling
[og-manifest]: https://github.com/jarondl/OxygenGuide-Android/blob/new_zip_handling/AndroidManifest.xml#L27
[og-provider]: https://github.com/jarondl/OxygenGuide-Android/blob/new_zip_handling/src/org/github/OxygenGuide/OxygenProvider.java
