# Blazor-Learnings
Just my personal learnings on how to use Blazor framework

## Navigation
URLs on pages need to be rooted (e.g. @page "/home"). When navigating using the NavigationManager the URL should not be rooted (e.g. NavigationManager.NavigateTo("home");). If the URL given to the NavigateTo method starts with a "/", vanigation won't work if the app is published to an IIS application in a sub folder of a IIS website.
