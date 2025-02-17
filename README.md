# eBPF-DexDumper
Android dexDumper based on eBPF

* Undetectable
* Passive dump

Show: https://blog.lleavesg.top/article/eBPFDexDumper

## Usage

**Test Env: Android 13 Pixel6**

**If other Android version , please fix the code and Compile.**

**Delete `/data/app/xxxx/xxxx-packagename/oat` folder first(check by `pm path packagename`), used to delete oat optimization content, to avoid the inability to dump or dump out `cdex`, etc.**

```
Usage: ./eBPFDexDumper <uid> <pathToLibart> <offsetExecute(hex)> <offsetExecuteNterpImpl(hex)> <offsetVerifyClass(hex)> <outputPath>
Example ( if Auto get offset ): ./eBPFDexDumper 10244 /apex/com.android.art/lib64/libart.so 0 0 0 /data/local/tmp/dexfile
Example (if get offset failed): ./eBPFDexDumper 10244 /apex/com.android.art/lib64/libart.so 0x473E48 0x200090 0x3D9F18 /data/local/tmp/dexfile
```
**uid**: UID of App you want to dump

**pathToLibart**: `libart.so` path, check by cat `/proc/<pid>/maps`

**offsetExecute(hex)**: offset(hex) of `art::interpreter::Execute` in `libart.so`

**offsetExecuteNterpImpl(hex)**: offset(hex) of `ExecuteNterpImpl` in `libart.so`

**offsetVerifyClass(hex)**: offset(hex) of `art::verifier::ClassVerifier::VerifyClass` in `libart.so`

**outputPath**: dumped dex file path

>By default, the symbols of libart.so will be parsed automatically.
The three offsets can be filled in freely, but if they are not found, you need to specify them manually, so it is recommended to fill in all 0s or all the correct offsets.

![image](https://github.com/user-attachments/assets/43e9d9ac-c56c-4dd7-9349-8d4fed1b6207)
![image](https://github.com/user-attachments/assets/565d1761-baa2-42cc-99c6-47eae703fee1)


## Compile
fix ndk path and make

```
make
```

## Reference
https://github.com/cilium/ebpf

https://github.com/null-luo/btrace

https://blog.seeflower.dev/archives/84/#title-7

https://evilpan.com/2021/12/26/art-internal/

https://zhuanlan.zhihu.com/p/523692715

https://blog.csdn.net/weixin_47668107/article/details/114251185

https://juejin.cn/post/7045575502991458340

https://juejin.cn/post/7384992816906747913

https://blog.quarkslab.com/dji-the-art-of-obfuscation.html
