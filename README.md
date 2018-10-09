# openwrt-intel-iot-devkit
[Intel® IoT Developer Kit](https://github.com/intel-iot-devkit) packages for OpenWrt LEDE-17.01

## Description
These support the latest version of node.js.

## Usage
Replace OpenWrt official packages.

Add follow line to feeds.conf or feeds.conf.default
```
src-git inteliot https://github.com/nxhack/openwrt-intel-iot-devkit.git;lede-17.01
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
