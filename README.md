# Pre-compiled Mesa-Turnip-Zink

Packages with Turnip Zink compiled and ready to be used on the system.

# How to install?

Install the package using `dpkg -i mesa-turnip-zink-<version>-<arch>.deb` You will come across some necessary dependencies, just type `apt --fix-broken install -y` and wait for the package to be installed.Drivers are installed in `/opt/<arch>/turnip-zink-<version>`.

# How to use?

The drivers were thought to be used in the Box4Droid project, but you can perfectly use it in your RootFS, there are two options.

• The first option is to simply copy the `include`, `lib` and `share` folders to the `/usr` folder of your RootFS, with that you will already be using the drivers by default on your system.

• The second option is for you who want to debug an application and don't want to override the drivers already installed on your system, you can use [Mesa's environment variables](https://docs.mesa3d.org/envvars.html) for that, here's an example:

`DISPLAY=:1 LIBGL_DRIVERS_PATH="/opt/arm64/turnip-zink-775e42e6/lib/aarch64-linux-gnu/dri/" VK_ICD_FILENAMES=/opt/arm64/turnip-zink-775e42e6/share/vulkan/icd.d/freedreno_icd.aarch64.json MESA_VK_WSI_DEBUG=sw MESA_LOADER_DRIVER_OVERRIDE=zink glxheads`

# Credits

I want to say a huge thank you to a few people who made this possible.

I want to thank [Heasterian](https://github.com/Heasterian), this generous man who always helped me when I had any doubts when compiling the drivers.

I would also like to mention and thank JeezDisReez, he made and shared a patch on Termux Discord where it is possible to compile Turnip with only the "kgsl" flag.
