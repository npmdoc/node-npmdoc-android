# api documentation for  [android (v0.0.8)](https://github.com/benmonro/android)  [![npm package](https://img.shields.io/npm/v/npmdoc-android.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-android) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-android.svg)](https://travis-ci.org/npmdoc/node-npmdoc-android)
#### various android utils & commands for node

[![NPM](https://nodei.co/npm/android.png?downloads=true)](https://www.npmjs.com/package/android)

[![apidoc](https://npmdoc.github.io/node-npmdoc-android/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-android_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-android/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-android/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-android/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Ben Monro"
    },
    "bugs": {
        "url": "https://github.com/benmonro/android/issues"
    },
    "dependencies": {},
    "description": "various android utils & commands for node",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "a5b03de920d7437a34ccecee5ee127ef1e4495a9",
        "tarball": "https://registry.npmjs.org/android/-/android-0.0.8.tgz"
    },
    "gitHead": "e7eaa71d632007fc83ecd965c3098fb752c54c1e",
    "homepage": "https://github.com/benmonro/android",
    "keywords": [
        "android",
        "adb"
    ],
    "license": "BSD",
    "main": "android.js",
    "maintainers": [
        {
            "name": "benmonro",
            "email": "ben.monro@gmail.com"
        }
    ],
    "name": "android",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/benmonro/android.git"
    },
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "version": "0.0.8"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module android](#apidoc.module.android)
1.  [function <span class="apidocSignatureSpan">android.</span>firstDevice (callback)](#apidoc.element.android.firstDevice)
1.  [function <span class="apidocSignatureSpan">android.</span>install (pathToApk, completedCallback)](#apidoc.element.android.install)
1.  [function <span class="apidocSignatureSpan">android.</span>isInstalled (pattern, isInstalledCallback)](#apidoc.element.android.isInstalled)
1.  [function <span class="apidocSignatureSpan">android.</span>push (from, to, callback)](#apidoc.element.android.push)
1.  [function <span class="apidocSignatureSpan">android.</span>sendBroadcast (options, callback)](#apidoc.element.android.sendBroadcast)



# <a name="apidoc.module.android"></a>[module android](#apidoc.module.android)

#### <a name="apidoc.element.android.firstDevice"></a>[function <span class="apidocSignatureSpan">android.</span>firstDevice (callback)](#apidoc.element.android.firstDevice)
- description and source-code
```javascript
firstDevice = function (callback) {
    adbDevices = exec("adb devices", function (error, stdout, stderr) {

        var findDeviceId = /\n([\d\w\.\:]+)\s+/m;
        var match = findDeviceId.exec(stdout);

        console.log("adb devices:\n" + stdout);

        if (match != null) {
            console.log("found a device");
            callback(match[1]);
        } else {
            callback();
        }
    });
}
```
- example usage
```shell
...
'''javascript
var adb = require("android");
'''

Get attached device id
----------------------
'''javascript
adb.firstDevice(function(deviceId){
	if(deviceId) {
		//there's a device attached, do cool stuff
	} else {
		//no device attached
	}
});
'''
...
```

#### <a name="apidoc.element.android.install"></a>[function <span class="apidocSignatureSpan">android.</span>install (pathToApk, completedCallback)](#apidoc.element.android.install)
- description and source-code
```javascript
install = function (pathToApk, completedCallback) {


    sys.print("installing " + pathToApk);
    var install = "adb install " + pathToApk;

    exec(install, function (err, stdout, stderr) {
        sys.print("result of " + install + ": " + stdout);

        completedCallback();
    });

}
```
- example usage
```shell
...
});
'''

Installing an APK
-----------------

'''javascript
adb.install("/path/to/my.apk", function() {
	//do cool stuff
});
'''

Pushing a file
--------------
'''javascript
...
```

#### <a name="apidoc.element.android.isInstalled"></a>[function <span class="apidocSignatureSpan">android.</span>isInstalled (pattern, isInstalledCallback)](#apidoc.element.android.isInstalled)
- description and source-code
```javascript
isInstalled = function (pattern, isInstalledCallback) {

    var isInstalledCommand = "adb shell pm list packages| grep package:" + pattern;
    console.log(isInstalledCommand);
    exec(isInstalledCommand, function (err, stdout, stderr) {
        console.log("result:\n" + stdout);

        isInstalledCallback(stdout.indexOf(pattern) >= 0);
    });

}
```
- example usage
```shell
...
	}
});
'''

Checking to see if a package is installed (wildcards allowed)
-------------------------------------------------------------
'''javascript
adb.isInstalled("com.example.*", function(isInstalled) {
	if(isInstalled) {
		//do cool stuff
	}
});
'''

Installing an APK
...
```

#### <a name="apidoc.element.android.push"></a>[function <span class="apidocSignatureSpan">android.</span>push (from, to, callback)](#apidoc.element.android.push)
- description and source-code
```javascript
push = function (from, to, callback) {
    exec("adb push " + from + " " + to, function(error, stdout, stderr){
        callback(error);
    });
}
```
- example usage
```shell
...
	//do cool stuff
});
'''

Pushing a file
--------------
'''javascript
adb.push("/path/to/src", "/path/to/target", function (err) {
	if(!err) {
		//do cool stuff
	}
});
'''

Sending a broadcast
...
```

#### <a name="apidoc.element.android.sendBroadcast"></a>[function <span class="apidocSignatureSpan">android.</span>sendBroadcast (options, callback)](#apidoc.element.android.sendBroadcast)
- description and source-code
```javascript
sendBroadcast = function (options, callback) {
    var extras = "";

    for (key in options.extras) {
        extras += " -e \"" + key + "\" " + options.extras[key];
    }

    var broadcastCmd = "adb shell am broadcast -a \"" + options.action + "\"" + extras;
    console.log("sending command: " + broadcastCmd);
    exec(broadcastCmd, function (error, stdout, stderr) {

            var dataMatch = (/data="(\{.*\})"/m).exec(stdout);
            var response = {};
            if (dataMatch) {
                response.data = dataMatch[1];
                response.message = stdout;
            }
            callback(response);
        }
    );
}
```
- example usage
```shell
...
'''

Sending a broadcast
-------------------
'''javascript
var options = {action:"com.example.ACTION_JACKSON", extras:{key:"lime", pie: "good"};

adb.sendBroadcast(options, function(response){
	console.log("response data: " + response.data);
	console.log("response message: " + response.message);
});
'''
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
