# openwrt-intel-iot-devkit
[Intel® IoT Developer Kit](https://github.com/intel-iot-devkit) packages for OpenWrt

## Description
These support node.js v6.x and v8.x. (for OpenWrt 15.01 Chaos Calmer branch)

## Usage
Replace OpenWrt official packages.

Add follow line to feeds.conf or feeds.conf.default
```
src-git inteliot https://github.com/nxhack/openwrt-intel-iot-devkit.git;for-15.05
```

Run
```
./scripts/feeds update inteliot
rm ./package/feeds/packages/swig
rm ./package/feeds/packages/libmraa
rm ./package/feeds/packages/libupm
./scripts/feeds install -a -p inteliot
```

## License
See [LICENSE](LICENSE) file.
