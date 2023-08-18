# What is Smidge?

Smidge is an effective tool used to boost the performance of web applications and improve the user experience.

## What is Bundling-Minification?
Bundling and minification shorten the load times of web applications, helping users access faster and have a better experience. It also reduces users' data usage as less data transfer is required. These two optimization techniques are widely used in modern web development processes and help increase the competitiveness of websites.

### What is Bundling?
Bundling is an optimization method that reduces download time by combining multiple files at the same time. Bundling creates a smaller number of larger files. In this way, all resources are downloaded in a single HTTP request, reducing the loading time of the web page. All the CSS and JavaScript code required for the web application is collected in a single file, so users can view the page faster.

### What is Minification?
Minification is a process used to optimize the source code files of a web application. This process edits code such as CSS, JavaScript and HTML to remove unnecessary characters, spaces and line breaks. It shortens variable names and transforms the code to take up less space without affecting functionality.

````csharp
app.UseSmidge(bundle =>
{
    bundle.CreateJs("my-js-bundle", "~/js/").WithEnvironmentOptions(BundleEnvironmentOptions.Create().ForDebug(builder => builder.EnableCompositeProcessing().EnableFileWatcher().SetCacheBusterType<AppDomainLifetimeCacheBuster>().CacheControlOptions(enableEtag: false, cacheControlMaxAge: 0)).Build());
});
````

````app.UseSmidge````: Used to add middleware so that the Smidge library can be used in your .NET Core application. This middleware allows JavaScript and CSS files to be bundled and processed when serving them to clients.

````bundle.CreateJs("my-js-bundle", "~/js/")````: The CreateJs method is used to create a new JavaScript bundle. Here, a bundle named "my-js-bundle" is created. The contents of the bundle are taken from the JavaScript files in the "~/js/" folder. So, this bundle will contain all the JavaScript files in the ~/js/ folder.

````.WithEnvironmentOptions(BundleEnvironmentOptions.Create().ForDebug(builder => ...).Build())````: This line is used to configure various environment options for the bundle's build. Here, the package's environmental options are configured with the ForDebug method. The following options are defined in the configuration:

````EnableCompositeProcessing()````: This allows packages to process duplicate structures whose contents in subfiles contain multiple files.

````EnableFileWatcher()````: This enables file watcher to detect changes during development.

````SetCacheBusterType<AppDomainLifetimeCacheBuster>()````: This sets the cache refresh method to ensure cache consistency. AppDomainLifetimeCacheBuster is used here, which is intended to keep the cache for the lifetime of the application domain. That is, it is cached when the app starts and the cache is cleared when the app is closed.

````CacheControlOptions(enableEtag: false, cacheControlMaxAge: 0)````: This is used to configure the Cache-Control and ETag header values. Here, ETag is disabled for caching (false) and the duration of the Cache-Control header is set to 0, which means that the file should not always be cached.
