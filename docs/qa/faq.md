## FAQ

## 0. where is the plugins

```
# macOS
$ open ~/.sdkbox

# windows
> explorer %systemdrive%%homepath%\.sdkbox
```

## 1. How to download specific plugin version

```
$ sdkbox list --json # will list all info

## template download link
# http://download.sdkbox.com/installer/v1/sdkbox-{plugin}_{version}.tar.gz

## facebook as example
# http://download.sdkbox.com/installer/v1/sdkbox-facebook_v2.6.0.1.tar.gz

# download it
$ curl http://download.sdkbox.com/installer/v1/sdkbox-facebook_v2.6.0.1.tar.gz -o ~/.sdkbox/plugins/sdkbox-facebook_v2.6.0.1.tar.gz
$ tar xf ~/.sdkbox/plugins/sdkbox-facebook_v2.5.1.0.tar.gz -C ~/.sdkbox/plugins/
```

## 2. How to install specific plugin version

```
## macOS user
$ sdkbox import ~/.sdkbox/plugins/sdkbox-facebook_v2.5.1.0 -p /path/to/your/project/root

# cocos creator
$ sdkbox import ~/.sdkbox/plugins/sdkbox-facebook_v2.5.1.0 -p /path/to/jsb/build/jsb-link
# or
$ sdkbox import ~/.sdkbox/plugins/sdkbox-facebook_v2.5.1.0 -p /path/to/jsb/build/jsb-default

## windows user
sdkbox import C:\Users\admin\.sdkbox\plugins\sdkbox-facebook_v2.6.0.0 -p Z:\test\ccc222\build\jsb-link --nohelp
```
