[![Super-Linter](https://github.com/RaspAP/plugins/actions/workflows/linter.yml/badge.svg)](https://github.com/marketplace/actions/super-linter)

# RaspAP plugins
This repo contains [custom user plugins](https://docs.raspap.com/custom-plugins/) to extend RaspAP's core functionality. These guidelines exist to assist plugin authors with adding their plugins to RaspAP.

## Developer guidelines
We welcome contributions from plugin authors to the RaspAP plugins repository! Follow these steps make your plugin available to users of RaspAP.

### Requirements
1. Modify the `.gitmodules` file to include your plugin repository as a submodule.
2. Update the `manifest.json` file by incrementing the `id` value and including your plugin's details.

### Detailed instructions
1. Create a new fork of this repository by choosing **Fork > Create a new fork**.
2. When this is done, clone it:
   ```
   git clone https://github.com/<your-username>/plugins.git
   cd plugins
   ```
3. Add your plugin as a submodule:
   ```
   git submodule add https://github.com/<your-plugin-repo>
   ```
4. Verify that `.gitmodules` now contains an entry similar to:
   ```
   [submodule "<plugin-name>"]
        path = <plugin-name>
        url = https://github.com/<your-plugin-repo>
   ```
5. Add your plugin to the `manifest.json` file. Increment the `id` value, then add your plugin's details in JSON format:
   
   ```
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
      }
    }
   ...
   ```
6. Commit and push your changes:
   ```
   git commit -am "Add <plugin-name> to submodules and update manifest.json"
   git push
   ```
7. Open a pull request in this repository by choosing **Pull requests > New pull request**. Choose "Compare across forks" and select your fork and branch. Create the pull request with a descriptive title and summary of your changes.

### Notes
Plugin submissions are tested and validated before they're included in the RaspAP plugins repo. The `plugins.manifest` is added as a dependency to the [main RaspAP respository](https://github.com/RaspAP/raspap-webgui). If approved, your plugin will be available to users via RaspAP's plugin manager in the next general release.
