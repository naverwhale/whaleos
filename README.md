# WhaleOS Opensource

## Build whaleos
- Checkout chromium
```
mkdir chromium && cd chromium && vi .gclient
```
- Create .gclient file
```
solutions = [
  {
    "name": "src",
    "url": "https://chromium.googlesource.com/chromium/src.git@120.0.6099.302",
    "managed": False,
    "custom_deps": {},
    "custom_vars": {},
  },
]
target_os = ["chromeos"]
```
```
gclient sync
```
- Checkout whaleos and build
```
mkdir whaleos && cd whaleos
repo init -u git@github.com:naverwhale/whaleos.git -b main
repo sync
cros_sdk --chrome_root ../chromium
exit
cd manifest
export BOARD=whalebook
./build_whaleos test
```

## Run whale
- ssh to whaleos device and remount root with RW
```
mount -o rw,remount /
rm -rf /opt/google/chrome
```
- Copy whale binary to /opt/google/chrome
```
wget https://github.com/naverwhale/whaleos/releases/download/r120/chrome.tar.gz
tar xzvf chrome.tar.gz
scp -r chrome ${DEVICE_IP}:/opt/google/
```
- Reboot your whaleos device

# License
See LICENSE files in each directories (find . -name 'LICENSE')
