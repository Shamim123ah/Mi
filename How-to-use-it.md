## Installation
1. Make sure you have [Magisk](https://topjohnwu.github.io/Magisk/install.html) 23.0+ and [Riru](https://github.com/RikkaApps/Riru#install) 25.0+ installed on your device.
1. Go to Magisk's `Modules` tab, search and install LSPosed.
1. Reboot your device and wait for a while, you will see the LSPosed icon.
1. Launch LSPosed and check the activation status.

### Install & Activate Modules
1. LSPosed is a framework and it cannot work without modules. You can browser from the `Repository` page from the app or the [web](http://modules.lsposed.org/).
1. Download and install modules as normal apps.
1. After installation, go to LSPosed's `Modules` page and click the module you installed, tick the enable switch.
1. Select apps to which the modules should apply. Most of the modules now support displaying recommended scope, which LSPosed will select automatically.
1. Some obsolete modules need to inject into each app. It's so dangerous that LSPosed doesn't support `Select All` and requires the user to tick each app one by one manually (the same policy as Magisk Hide).

### Dual App / Multiuser Support
1. Before that, you should notice that many obsolete modules were born in the era when multiuser was not popular and thus they may not support multiuser well. There's nothing LSPosed could do to make them work on multiuser mode.
1. Moreover, the LSPosed Manager will only work on the primary user, and it can manage modules and apps from all users. You DON'T have to install it on the other users.
1. As long as your device has multiple users, LSPosed shows a tab for each user on the `Modules` page. Switch between tabs to manager modules from different users.
1. You should install modules to the user on which you want it to work. You can do it manually (recommended) by switching to that user and install the modules. Or you can do it via LSPosed Manager (not recommended as long as you can do it manually).

