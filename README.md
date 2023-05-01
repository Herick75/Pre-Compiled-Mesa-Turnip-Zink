# Pre-compiled Mesa-Turnip-Zink

Packages with Turnip Zink compiled and ready to be used on the system.

# How to install?

Install the package using `dpkg -i mesa-turnip-zink-<version>-<arch>.deb` You will come across some necessary dependencies, just type apt --fix-broken install -y and wait for the package to be installed.Drivers are installed in `/opt/<arch>/turnip-zink-<version>`.

# How to use?

The drivers were thought to be used in the Box4Droid project, but you can perfectly use it in your RootFS, there are two options.

• The first option is to simply copy the `include`, `lib` and `share` folders to the `/usr` folder of your RootFS, with that you will already be using the drivers by default on your system.

• The second option is for you who want to debug an application and don't want to override the drivers already installed on your system, you can use Mesa's environment variables for that, here's an example:
