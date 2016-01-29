## Introduction ##

If you are interested in creating a plugin for dicompyler, and have never created one before, first see the [PluginDevelopmentGuide](http://code.google.com/p/dicompyler/wiki/PluginDevelopmentGuide) on the dicompyler wiki.

Once you have decided you want to create a plugin and would like to share it with the dicompyler community, please make a post on the [dicompyler Google Group](http://groups.google.com/group/dicompyler). We will then grant you access to the repository.

## Getting Started ##

  1. Checkout the repository - instructions can be found [here](http://code.google.com/p/dicompyler-plugins/source/checkout)
  1. Once you have obtained a local checkout, please make a folder with your plugin name in the 'plugins' folder. You can commit all your files to that folder.
  1. Only make changes to your plugin. If you have more than one plugin, feel free to edit them, but if possible make separate commits so we can track changes.
  1. Make sure you run `hg pull` and `hg update` before committing so that new heads aren't inadvertently created. (More conveniently you could run `hg fetch` instead - see [here](http://mercurial.selenic.com/wiki/FetchExtension).)

## Differences from Standalone Plugins ##

There are a few differences for repository plugins vs. regular plugins, which are detailed as follows:

### Plugin Folder Support ###

In order for dicompyler to support plugins located within a folder (such as repository plugins), you need to to add an init.py in your plugin folder that has the following lines:

```
# __init__.py

from modulename import pluginProperties, plugin
```

where `modulename` is your main plugin module name.

### Documentation ###

To document your plugin, create a wiki page for it, ideally with the same name as your plugin. Another option is to make a _readme_ file and place it within your repository.

Either way, add the following line to your `pluginProperties` dictionary with the full URL of your wiki page or the name of your readme file, such as:

```
props['documentation'] = 'http://code.google.com/p/dicompyler-plugins/wiki/pluginname'
```

If you prefer to host your documentation somewhere else, you may use that URL instead.

The link or readme file will be displayed to the user in the plugin browser.


### License ###

Since the plugin source code is publicly accessible, each plugin **should** be released under a specific software license. A list of suggested licenses can be found [here](http://www.opensource.org/licenses/category).

Place the license file in your plugin folder and add the following line to your `pluginProperties` dictionary with the filename:

```
props['license'] = 'license.txt'
```

where `license.txt` is your license filename.

_**Note**_: If you don't explicitly indicate what license your plugin uses, it will be assumed that it follows the same licensing scheme as dicompyler, which is released under the [New BSD License](http://www.opensource.org/licenses/bsd-license.php).

### Icon ###

If you desire, you can have a small icon (32x32) that will be displayed in the plugin browser. Place the image in your plugin folder and add the following line to your `pluginProperties` dictionary with the filename:

```
props['icon'] = 'image.png'
```

where `image.png` is your image filename.

## Release Process ##

When you are ready to make a release for your plugin, you will execute a script in the main repository folder that will do the following:
  1. Extract the relevant infomation from your plugin (basically plugin properties and a list of required files)
  1. Create a source zip file
  1. Update the repository listing text file with the latest version of your plugin

## Example ##

The plugin _scaledose_ in the repository can serve as a good starting point for understanding the directory layout and modifications discussed above.

## Testing ##

One way to make using the plugin repository easier (at least on Mac/Linux) to test is to make a symbolic link to the plugins folder from your repository checkout to the user plugins folder (example is on Linux):

  * First, delete the plugins folder in the _~/.dicompyler/_ folder (make sure you save any plugins you want from this folder).
  * Then, in the _~/.dicompyler/_ folder execute:

```
ln -s ~/Projects/python/dicompyler-plugins/plugins plugins
```

  * Any plugins that are in the repository will now show up in your copy of dicompyler automatically. By updating to the latest plugin repository source, you will also gain the latest versions of all the plugins.