# openwrt-eclipse-iot-devkit
[Eclipse IoT Project](https://projects.eclipse.org/projects/iot) packages for OpenWrt

## Description
These support the latest version of node.js.

## Usage
Replace OpenWrt official packages.

Add follow line to feeds.conf or feeds.conf.default
```
src-git eclipseiot https://github.com/nxhack/openwrt-eclipse-iot-devkit.git
```

Run
```
./scripts/feeds update eclipseiot
rm ./package/feeds/packages/libmraa
rm ./package/feeds/packages/libupm
./scripts/feeds install -a -p eclipseiot
```

## License
See [LICENSE](LICENSE) file.
