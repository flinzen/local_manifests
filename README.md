## How to compile Android 6.0 for Pine A64

1. Checkout http://source.android.com/source/downloading.html
1. Create a new directory:
  ```
  mkdir android
  cd android
  ```

2. Initialize manifests:
  ```
  repo init -u https://android.googlesource.com/platform/manifest -b android-6.0.1_r74 --depth=1
  git clone https://github.com/flinzen/local_manifests -b my-hacks .repo/local_manifests
  ```

3. Checkout sources:
  ```
  repo sync -c
  ```

3.1.
```
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
apt install git-lfs
```

3.2 In Android directory
```
cd vendor/opengapps/sources/
for d in ./*/ ; do (cd  && git lfs pull); done
```

If nothing happens or error appears checkout master branch in subdirectories and use ```git lfs pull``` command manually 

4. Compile sources:
  ```
  source build/envsetup.sh
  # tulip_chihpd-eng: use for normal Android build with Launcher
  # tulip_chiphd_atv-eng: use for Android TV build with Leanback Launcher
  lunch tulip_chiphd-eng
  make
  ```

5. Create SD card image:
  ```
  sdcard_image pine64_android_6.img.gz sopine
  ```

## Changes

I did backport minimal amount of Allwinner changes to make it run.
You can see a commit history.

Callahan633: I had changed remote for kernel sources with fixes for WM8904 external codec on I2S Euler Bus (based on: https://github.com/looperlative/linux-pine64-armbian/commits/ramstadt) and added to manifest Gapps from their new remote on gitlab

## Author

Kamil Trzciński (ayufan@ayufan.eu)
