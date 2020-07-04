# Plugins
## Setting up a new Plugin
1. open the Plugins Window  
   ![](../Images/Plugin/Creation/01_Plugins.png)

2. click on create new plugin  
   ![](../Images/Plugin/Creation/02_NewPlugin.png)

3. select a template for the plugin and fill in the name of the plugin, the author and a description  
    ![](../Images/Plugin/Creation/03_PluginSettings.png)

4. To create a c++ class from within Unreal you have to select the correct project/ plugin. It will be located at the path: ./ProjectName/Plugins/PluginName/Source/Public/YourFile.h and ./ProjectName/Plugins/PluginName/Source/Public/YourFile.cpp  
   ![](../Images/Plugin/Creation/04_NewClass.png)

## Managing Plugin Dependency
We will need plugins to depend on each other (mostly on PMSCore). For this we will have to change some settings in the plugin. These changes are only necessary in the plugin that depends on another one.

For the following example there are 2 plugins. PMSCore and PMSDetection. PMSDetection depends on PMSCore.

1. Change the uplugin file of PMSDetection. After the "Modules" declaration we will have to add plugins on which this plugin depends on.  
    ![](../Images/Plugin/Dependency/01_uplugin.png)

2. Add the required dependencies in the Build.cs file.  
    ![](../Images/Plugin/Dependency/02_build.png)

source: [AntimonyFox: Plugin dependent on another plugin](https://answers.unrealengine.com/questions/573095/plugin-dependent-on-another-plugin.html)