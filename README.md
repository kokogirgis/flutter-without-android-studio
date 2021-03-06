# flutter-without-android-studio
this is a step by step documentation on how to use flutter from scratch without android studio

**DISCLAIMER:** this method meant for those who have very low-end PCs and those who love playing with command-line tools, if you can't find yourself there i highly encourge you to stop here and use the official and the well-supported Android Studio method.

## What do we need?
* **openjdk-11-jdk**
* **android-sdk** package (from your repo package manager for example) to provide the basic directory structure, for ubuntu users you can use aptitude to install it `sudo apt install android-sdk`
* [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager) download it from [here](https://developer.android.com/studio#downloads) and seach for `command-line-tools` 
* **Flutter-sdk** download it from [here](https://flutter.dev/docs/get-started/install/linux#get-sdk) 
* [vim](https://github.com/vim/vim) / [neovim](https://github.com/neovim/neovim) or [vscode](https://github.com/microsoft/vscode) or any text editor of your choise, i will use neovim as my text-editor, but you don't really have to
* For (neo)vim users i recommend installing a plug-ins manager (i.e. vim-plug) [coc](https://github.com/neoclide/coc.nvim) then [coc-flutter](https://github.com/iamcco/coc-flutter) very useful plugins while dealing with flutter
* For vs-code users install Flutter plug-in

## Steps:
### Step 1 (perpare your directory structure):
Assuming you had followd the [What do we need](https://github.com/A-Siam/flutter-without-android-studio#what-do-we-need) section above you will have `/usr/lib/android-sdk` directory, create cmdline-tools directory inside it 
```bash
sudo mkdir /usr/lib/android-sdk/cmdline-tools
# unzip the content of command line tools to that folder
sudo unzip /path/for/your/command-line/tools/zip/commandlinetools-linux-*.zip /usr/lib/android-sdk/cmdline-tools
# link the content of /usr/lib/android-sdk/cmdline-tools/tools/bin to /usr/lib/android-sdk/tools/bin 
# because flutter will seach for "/usr/lib/android-sdk/tools/bin" when it need the sdkmanager
sudo ln -s /usr/lib/android-sdk/cmdline-tools/tools/bin/* /usr/lib/android-sdk/tools/bin
# define the environmental variables and add the command line tools to path
# NOTE: i will use ~/.profile as a matter of preference but most people will prefer using .xrc (where x is (zsh, bash, ...etc)) 
echo -e "export ANDROID_SDK_ROOT=/usr/lib/android-sdk\nexport PATH=\$ANDROID_SDK_ROOT/cmdline-tools/tools/bin:\$PATH" >> ~/.profile
```
### Step 2 (Download android-sdk):
This is a list of the very essential packages you should have to be able to run you app

**NOTE:** you will definitely need more than these packages for production (i.e. the google play packages)
```
  Path                        | Version | Description                    | Location                    
  -------                     | ------- | -------                        | -------                     
  build-tools;28.0.3          | 28.0.3  | Android SDK Build-Tools 28.0.3 | build-tools/28.0.3/         
  extras;android;m2repository | 47.0.0  | Android Support Repository     | extras/android/m2repository/
  extras;google;m2repository  | 58      | Google Repository              | extras/google/m2repository/ 
  patcher;v4                  | 1       | SDK Patch Applier v4           | patcher/v4/                 
  platform-tools              | 30.0.0  | Android SDK Platform-Tools     | platform-tools/             
  platforms;android-28        | 6       | Android SDK Platform 28        | platforms/android-28/       
  tools                       | 25.0.0  | Android SDK Tools              | tools/                    
  ```
  so you will download these packages 
  ```bash
  # the packages i have ignored should already exist in on your machine
  # Notice that i didn't install the latest versions ,it won't work ,it's a known issue and flutter's team are working on it
  sudo `which sdkmanager` "build-tools;28.0.3" "extras;android;m2repository" "extras;google;m2repository" "platform-tools" "platforms;android-28"
  # then accept the licenses
  sdkmanager --licenses
  ```
### Step 3 (The flutter side):
#### Step 3.1 (flutter doctor check)
first follow the instruction in the download like 
then run `flutter doctor` the output should look like this
```
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, v1.12.13+hotfix.9, on Linux, locale en_US.UTF-8)
 
[!] Android toolchain - develop for Android devices (Android SDK version 28.0.3)
    ! Some Android licenses not accepted.  To resolve this, run: flutter doctor
      --android-licenses
[!] Android Studio (not installed)
[!] Connected device
    ! No devices available

! Doctor found issues in 3 categories.
```
these issue are ok if something really went wrong flutter will inform you when you run 
#### Step 3.2 (testing):
Any serious errors should appear here
```
flutter create my_app # This will take a long time in the first execution so don't worry
cd ./my_app
flutter run -v 
```
if everything went ok your app will run on your device as normal
### Step 4 (prepare you text editor):
#### Step 4.1 (vs-code users)
All you have to do is to install `dart` and `flutter` plugins, now you are ready to go

#### Step 4.2 (vim users)
follow the installation instructions from you choosen plug-ins manager then install `coc` and `coc-flutter` mentioned above then you are ready to go

Tested on **UBUNTU 20.04** 
