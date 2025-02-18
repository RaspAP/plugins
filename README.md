[![Super-Linter](https://github.com/RaspAP/plugins/actions/workflows/linter.yml/badge.svg)](https://github.com/marketplace/actions/super-linter)

# RaspAP plugins
This repo tracks [custom user plugins](https://docs.raspap.com/custom-plugins/) for extending RaspAP's core functionality. These guidelines exist to assist plugin authors with adding their plugins to RaspAP.

## Developer guidelines
All developers are welcome and encouraged to add their plugins to the RaspAP plugins repository! Follow these steps make your plugin available to users of RaspAP.

### How it works
This repo is included as a dependency of the [main RaspAP respository](https://github.com/RaspAP/raspap-webgui). RaspAP's `PluginManager` and `PluginInstaller` components parse the `manifest.json` file in this repo to present the user with a list of available plugins, and indicate which (if any) are already installed on their system.

Adding your plugin for inclusion by RaspAP is done by incrementing the `id` value in `manifest.json` and adding your plugin's details in JSON format.

1. Create a new fork of this repository by choosing **Fork > Create a new fork**.
2. When this is done, clone your fork and change into the source folder:
   ```
   git clone https://github.com/<your-username>/plugins.git
   cd plugins
   ```
3. Add your plugin to the `manifest.json` file. Increment the `id` value, then add your plugin's details in JSON format. You may use the previously approved plugin in this file as a template. For example:
   
   ```
   {
     "id": "<increment-last-id>",
     "name": "Amazing Plugin",
     "version": "v1.0.0",
     "description": "An amazing plugin to extend RaspAP",
     "author": "A. Plugin Author",
     "author_uri": "https://github.com/",
     "plugin_uri": "https://github.com/PluginAuthor/AmazingPlugin",
     "license": "GPL-3.0",
     "namespace": "RaspAP\\Plugins\\AmazingPlugin",
     "configuration": [
       {
         "source": "config/myplugin.conf",
         "destination": "/etc/myplugin.conf"
       }
     ],
     "default_locale": "en_US",
     "dependencies": {
       "some-apt-package": "1.0"
     },
     "icon": "fas fa-meteor",
     "manifest_version": "1.0",
     "sudoers": [
       "www-data ALL=(ALL) NOPASSWD:/bin/systemctl * myplugin.service",
       "www-data ALL=(ALL) NOPASSWD:/bin/cat /etc/myplugin.conf",
       "www-data ALL=(ALL) NOPASSWD:/bin/cp /tmp/myplugin.conf /etc/myplugin.conf"
     ],
     "user_nonprivileged": {
       "name": "pluginuser",
       "pass": "pluginpass"
     },
      "install_path": "plugins"
    }
   ```
   
4. Commit and push your changes:
   ```
   git commit -am "Add <plugin-name> to manifest.json"
   git push
   ```
5. Open a pull request in this repository by choosing **Pull requests > New pull request**. Choose "Compare across forks" and select your fork and branch. Create the pull request with a descriptive title and summary of your changes. Submit your pull request for review. That's it!

### Notes
The `manifest.json` file is automatically validated by a JSON linter. Invalid JSON contained in a pull request will be flagged by the GitHub action. If your JSON is invalid, close the pull request, fix `manifest.json` (validate it beforehand with your code editor or by using one of many [online tools](https://jsonlint.com/)), commit the change and submit a new pull request.

All plugin submissions are thoroughly tested and validated prior to inclusion in the RaspAP plugins repo. If approved, your plugin will immediately be made available to users via RaspAP's Plugin Manager UI.
