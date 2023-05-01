# Pre-compiled Mesa-Turnip-Zink

Packages with Turnip Zink compiled and ready to be used on the system.

# How to install?

Install the package using `dpkg -i mesa-turnip-zink-<version>-<arch>.deb` You will come across some necessary dependencies, just type `apt --fix-broken install -y` and wait for the package to be installed.Drivers are installed in `/opt/<arch>/turnip-zink-<version>`.

**Only tested on Ubuntu 22.04 (Jammy)**

## Notes about armhf packages on arm64 RootFS 

If you want to install armhf drivers on arm64, you will need to add multiarch support in your RootFS, for that type `dpkg --add-architecture armhf` and then type `apt update`, after that you will be able to install the drivers .

# How to use?

The drivers were thought to be used in the [Box4Droid](https://github.com/Herick75/Box4Droid) project, but you can perfectly use it in your RootFS, there are two options.

• The first option is to simply copy the `include`, `lib` and `share` folders to the `/usr` folder of your RootFS, with that you will already be using the drivers by default on your system.

You will need to use some Mesa environment variables to use the drivers, it is recommended to add them in the `.bashrc` file so you don't have to export them every time you start a session in your RootFS. The variables I recommend adding are `export MESA_VK_WSI_DEBUG=sw`, `export MESA_LOADER_DRIVER_OVERRIDE=zink`, `export MESA_GL_VERSION_OVERRIDE=4.6COMPAT`

• The second option is for you who want to debug an application and don't want to override the drivers already installed on your system, you can use [Mesa environment variables](https://docs.mesa3d.org/envvars.html) for that, here's an example:

`DISPLAY=:1 LIBGL_DRIVERS_PATH="/opt/arm64/turnip-zink-775e42e6/lib/aarch64-linux-gnu/dri/" VK_ICD_FILENAMES=/opt/arm64/turnip-zink-775e42e6/share/vulkan/icd.d/freedreno_icd.aarch64.json MESA_VK_WSI_DEBUG=sw MESA_LOADER_DRIVER_OVERRIDE=zink glxheads`

# Credits

I want to say a huge thank you to a few people who made this possible.

I want to thank [Heasterian](https://github.com/Heasterian), this generous man who always helped me when I had any doubts when compiling the drivers.

I also used the Cross Compile method that Heasterian provided in their Box86-64-on-SD845-mobian repository [here](https://github.com/Heasterian/Box86-64-on-SD845-mobian/blob/main/docs/PREREQUISITES.md#prerequisites).

I would also like to mention and thank JeezDisReez, he made and shared a patch on Termux Discord where it is possible to compile Turnip with only the "kgsl" flag.

And thanks to the [Mesa](https://gitlab.freedesktop.org/mesa/mesa) devs for developing the drivers.
