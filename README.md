# mkfatfs
Tool to build and unpack [FATFS](https://github.com/jkearins/ESP32_mkfatfs) images.


## Usage

```

  in windows:

  mkfatfs  {-c <pack_dir>|-u <dest_dir>|-l|-i} [-d <0-5>] [-b <number>]
            [-p <number>] [-s <number>] [--] [--version] [-t <fstype>] [-h]
            <image_file>

  in linux:
  ./mkfatfs  {-c <pack_dir>|-u <dest_dir>|-l|-i} [-d <0-5>] [-b <number>]
          [-p <number>] [-s <number>] [--] [--version] [-t <fstype>] [-h]
          <image_file>

eg:
pack:
windows:
mkfatfs.exe -c Test -s 0x200000 -t littlefs test.bin
linux: 
./mkfatfs -c Test -s 0x200000 -t littlefs test.bin

unpack:
windows:
mkfatfs.exe -u Test -s 0 -t littlefs test.bin
linux:
./mkfatfs -u Test -s 0 -t littlefs test.bin

Where: 

   -c <pack_dir>,  --create <pack_dir>
     (OR required)  create fatfs image from a directory
         -- OR --
   -u <dest_dir>,  --unpack <dest_dir>
     (OR required)  unpack fatfs image to a directory
         -- OR --
   -l,  --list
     (OR required)  list files in fatfs image
         -- OR --
   -i,  --visualize
     (OR required)  visualize fatfs image


   -d <0-5>,  --debug <0-5>
     Debug level. 0 means no debug output.

   -b <number>,  --block <number>
     fs block size, in bytes

   -p <number>,  --page <number>
     fs page size, in bytes

   -s <number>,  --size <number>
     fs image size, in bytes

   -t <fstype> --type <fstype>
     fs type, surport fatfs and littlefs

   --,  --ignore_rest
     Ignores the rest of the labeled arguments following this flag.

   --version
     Displays version information and exits.

   -h,  --help
     Displays usage information and exits.

   <image_file>
     (required)  fatfs image file


```
## Build

You need gcc (≥4.8) or clang(≥600.0.57), and make. On Windows, use MinGW.
You need cmake (≥3.0.0).
Youn can develop in vscode. install extension CMake and CMake Tools.
More help for build project, please read the extension's help.
in linux:
  cd mkfatfs
  cmake .
  make

## License

MIT

## To do

- [ ] Flag -u is not released yet
- [ ] Flag -l is not released yet
- [ ] Flag -i is not released yet
- [ ] Add more debug output and print FATFS debug output
- [ ] Error handling
- [ ] Determine the image size automatically when opening a file
- [ ] Code cleanup
