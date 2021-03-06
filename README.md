# Blazor-Learnings
Just my personal learnings on how to use Blazor framework

## Development
### Navigation
URLs on pages need to be rooted (e.g. @page "/home"). When navigating using the NavigationManager the URL should not be rooted (e.g. NavigationManager.NavigateTo("home");). If the URL given to the NavigateTo method starts with a "/", vanigation won't work if the app is published to an IIS application in a sub folder of a IIS website.

## Deployment
### Copy additional files
Not specific to blazor: If the project contains additional files (e.g. a .xml configuration file) one can simply add a new <ItemGroup> section to the project file. One example that copies the single file MyConfig.xml to a sub folder ConfigFiles:
  
    <ItemGroup>
      <_CustomFiles Include="$(MSBuildProjectDirectory)/MyConfig.xml" />
      <DotNetPublishFiles Include="@(_CustomFiles)">
        <DestinationRelativePath>ConfigFiles/%(Filename)%(Extension)</DestinationRelativePath>
      </DotNetPublishFiles>
    </ItemGroup>
    
### Publish profiles are MSBuild files
Not specific to blazor: To copy custom files into the publish directory depending on the publish profile, one can include statements like this into the .pubxml file as well:

    <ItemGroup>
      <_CustomFiles Include="$(MSBuildProjectDirectory)/MyConfig.Development.xml" />
      <DotNetPublishFiles Include="@(_CustomFiles)">
        <DestinationRelativePath>App_Start/MyConfig.xml</DestinationRelativePath>
      </DotNetPublishFiles>
    </ItemGroup>

That way one could create a seperate .pubxml file for each deployment destination and let each one inlude a different configuration.
