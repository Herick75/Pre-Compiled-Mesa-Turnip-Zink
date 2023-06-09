# Pre-compiled Mesa-Turnip-Zink

Packages with Turnip + Zink compiled and ready to be used on the system.

# How to install?

If you want to install armhf drivers on arm64, you will need to add multiarch support in your RootFS, type

`dpkg --add-architecture armhf ; apt update`

after that you will be able to install the drivers .

Install the package using 

`apt install ./mesa-turnip-zink-<version>-<arch>.deb`

Drivers are installed in `/opt/<arch>/turnip-zink-<version>`.

**Only tested on Ubuntu 22.04 (Jammy)**

# How to use?

The drivers were thought to be used in the [Box4Droid](https://github.com/Herick75/Box4Droid) project, but you can perfectly use it in your RootFS, there are two options.

- The first option is to simply copy the `include`, `lib` and `share` folders to the `/usr` folder of your RootFS, with that you will already be using the drivers by default on your system.

After copying the folders to the ```/usr``` directory, edit the file at ```/usr/share/vulkan/icd.d/freedreno_icd.arch.json``` (You can use the editor of your choice, in my case I used ```nano```).  Go down to line 4, and update the directory of the libvulkan_freedreno.so file, which is now in /usr/lib/arch/libvulkan_freedreno.so (Replace ```arch``` with ```arm-linux-gnueabihf``` or ```aarch64-linux-gnu```.

You will need to use some Mesa environment variables to use the drivers, it is recommended using [alias](https://www.geeksforgeeks.org/alias-command-in-linux-with-examples/) or export so you don't have to export them every time you start a new session in your RootFS. The variables I recommend adding are `MESA_VK_WSI_DEBUG=sw`, `MESA_LOADER_DRIVER_OVERRIDE=zink` and `MESA_GL_VERSION_OVERRIDE=4.6COMPAT`
- The second option is for you who want to debug an application and don't want to override the drivers already installed on your system, you can use [Mesa environment variables](https://docs.mesa3d.org/envvars.html) for that, here's an example:

```
export \
  LIBGL_DRIVERS_PATH="/opt/turnip-zink/arm64/lib/aarch64-linux-gnu/dri/:/opt/turnip-zink/armhf/lib/arm-linux-gnueabihf/dri/" \
  VK_ICD_FILENAMES="/opt/turnip-zink/arm64/share/vulkan/icd.d/freedreno_icd.aarch64.json:/opt/turnip-zink/armhf/share/vulkan/icd.d/freedreno_icd.d/freedreno_icd.armv8.2l.json" \
  MESA_VK_WSI_DEBUG=sw \
  MESA_LOADER_DRIVER_OVERRIDE=zink
  ```
  
- For Areno 610 :
  `TU_DEBUG=noconform`

# Credits

I want to say a huge thank you to a few people who made this possible.

I want to thank [Heasterian](https://github.com/Heasterian), this generous man who always helped me when I had any doubts when compiling the drivers.

I also used the Cross Compile method that **Heasterian** provided in their **Box86-64-on-SD845-mobian** repository [here](https://github.com/Heasterian/Box86-64-on-SD845-mobian/blob/main/docs/PREREQUISITES.md#prerequisites).

I would also like to mention and thank **JeezDisReez**, he shared a patch on Termux Discord where it is possible to compile Turnip with only the "kgsl" flag.

And thanks to the [Mesa](https://gitlab.freedesktop.org/mesa/mesa) devs for developing the drivers.
