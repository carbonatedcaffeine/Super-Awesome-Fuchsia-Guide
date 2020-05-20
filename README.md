# Super-Awesome-Fuchsia-Guide
For people who are new to developing with fuchsia!

## Chapter One: Getting Ready
You will need the following:
* A desktop or laptop running Debian 10 or Ubuntu 18.04 (for best experience and easiness)
* A fast internet connection (preferably ethernet)
* Patience

## Chapter Two: Fetching Fuchsia
Firstly you will need to get the dependencies to be able to fetch and build fuchsia. 

`sudo apt install build-essential curl git python unzip`

And also install ccache for faster build times. (it really helps, trust me)

`sudo apt install ccache`

Now it's time to get fetching! `cd` into the directory where you want your fuchsia build, if your unsure where to put it, your home directory should do nicely. And with that we shall start fetching!

`curl -s "https://fuchsia.googlesource.com/fuchsia/+/master/scripts/bootstrap?format=TEXT" | base64 --decode | bash`

If you didn't get any errors, congrats! Skip straight to chapter 3. If you got the cipd package error then click the link in your terminal and login with your google account and re-fetch (`jiri update`). It will only take a tick since you've already got the source.

### Chapter 2.5: Problems with fetching
Sometimes it doesn't go so smoothly... but thats okay! We'll get that sorted in a tick.

#### Jiri hooks fail

eg: `ERROR: "running hook(garnet-update) for project fuchsia" failed 3 times in a row, Last error: context deadline exceeded`

This happens when it takes too long to fetch a certain project that fuchsia needs (each project is given an amount of time to fetch) I'd recommend using ethernet to download the source or get closer to your wifi.

## Chapter 3: Lets Build
First off we need to set the build config...

`fx set core/workstation/bringup.x64/arm64` --ccache

eg: `fx set core.x64`

if you want to see the different configs you can build you can run these two commands

```
fx list-boards
fx list-products
```

Some other useful information:
* Worstation: Best for graphics and tinkering (if your unsure which one to use, use this one)
* Core: Best for command line hackery
* Bringup: Used for early development of porting devices`

Now once you've chosen your configuration it's time to actually build.

`fx build` 

Once it's done... it's time to test your build out.

## Chapter 4: Testing the build
The way we're going to test this build is with AEMU, which is an Android Emulator artifact that can run fushsia + graphics without actually paving it. Firt off make sure you have the Vulkan driver installed, you can find out how to install it here: https://github.com/lutris/docs/blob/master/InstallingDrivers.md (read carefully).

make sure it's working with `sudo apt install vulkan-utils && vulkaninfo`

and finnaly lauch aemu with `fx emu`. You can also add `--host-gpu` to use accelerated graphics. 

## Chapter 5: Paving (coming soon)
