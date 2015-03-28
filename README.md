# YeoPress Default Theme

This base theme is packed full of goodies to get your WordPress development process off the ground.  Not only does it come with a decent amount of WP Theme files, it also gets you setup with a `Gruntfile` with some goodies like LiveReload, Sass compilation and RequireJS support.

Once you have run the setup process with YeoPress, you are ready to start working with your theme.  So change directory into the theme directory and run grunt:

	$ cd wp-content/themes/your-theme-name-chosen-at-setup
	$ grunt

This will fire up the watch task which will listen for changes in your files and trigger the appropriate update tasks and will reload the browser via LiveReload.

## RequireJS

This theme integrates RequireJS for Javascript dependency management and lazy-loading.  There are two tasks built into the `Gruntfile` to help manage and build your require configuration: `bower` & `requirejs`.

### Bower Task

	$ grunt bower

The `bower` task will take any packages installed via Bower, and add them to the require config.  There is one caveat at the moment, because the `Gruntfile` is in the theme and not in the root of the site, the `baseDir` setting causes this task to build incorrect paths.  All that needs to be done is to remove the initial `../`'s that are added.  For example, here is the config after running the task:

	"baseUrl": "content/themes/yeopress/js",
	"paths": {
		"jquery": "../../../../js/vendor/jquery/jquery"
	}

What we really wanted was just the part that reads `vendor/jquery/jquery`, so just remove the part we don't need and you will be good to go:

	"baseUrl": "content/themes/yeopress/js",
	"paths": {
		"jquery": "vendor/jquery/jquery"
	}

### RequireJS Task

	$ grunt requirejs

The second task, `requirejs` is used to build an optimized require file.  By default the optimized file is output to `js/optimized.js`, but this can be changed in the `Gruntfile`.  For more information on how to configure this setting see [here](https://npmjs.org/package/grunt-contrib-requirejs) and [here](http://requirejs.org/docs/optimization.html).

## Build Task

	$ grunt build

This task builds an optimized version of the theme for production.  It runs the following tasks:

- jshint
- sass:production
- imagemin:production
- svgmin:production
- requirejs:production

For the image min tasks, the files are saved directly over the original files.  The sass production builds minified css for the live site in the css directory.  The only one that will take some configuration and a change to your php is the requirejs task.  This task generates optimized files using the `r.js` tool, and comes packaged to output one file called `optimized.min.js` which you would then need to enqueue through the WordPress `functions.php` file.

![image](http://wesleytodd.com/media/pages/index/yeopress.jpg)

# YeoPress

The officially un-official [Yeoman](https://github.com/yeoman/yeoman) Generator for [WordPress](http://wordpress.org/).  I magically take you from scratching your head wondering where to start, all the way to running the famous 5-minute install.  I have configuration options that will WOW you.  If you use Git, I can *git* you off the ground with WordPress as a submodule just by following a couple of prompts.  Have a custom base theme you always start your projects off with?  You can install that too, either straight from GitHub or by pointing me to a tarball.  Other things I do:

- Custom directory configuration
- Install WordPress as a Git submodule for easy version controlled updates
- Theme init hook for when you install a new theme
- Permission setting on install
- Create your database, all you have to do is make me a user
- Built in Vagrant configuration
- *New* Set custom defaults with `.yeopress` files
- *New* Environment based wp-config files, `local-config.php`

## How To Use

If you do not already have the Yeoman toolset installed do so now, and might as well install me at the same time *(NOTE: don't type the `$`)*:

	$ npm install -g yo generator-wordpress

While running if you get errors try running as super user:

	$ sudo npm install -g yo generator-wordpress

And run me:

	$ yo wordpress

Follow my prompts and WA-BAM....ASCII art!!!!

![image](http://wesleytodd.com/media/posts/yeopress-a-yeoman-generator-for-wordpress/yeopress-ascii-art.png)

### Advanced Usage

By specifying the `--advanced` flag you get access to more features:

- Vagrant: Sets up a Vagrant box using Puppet with all the requirements for running a WordPress site.
- WP version: Select a specific WordPress version to install
- Block external requests: Adds the `WP_HTTP_BLOCK_EXTERNAL` setting to config to lock down the admin
- Add core files to gitignore: Adds rules to the `.gitignore` file for the WordPress core files

### Reusing common settings

You probably want to be able to quickly zip through your install with similar settings for every project.  For example, you probably always want to use git but the default is no git.  You can define any custom defaults you want in `~/.yeopress`.  This file is just a json file with key-value pairs for the config settings you want.  Here is an example:

```json
{
	"git": true,
	"dbHost": "localhost",
	"dbName": "yeopress",
	"dbUser": "yeopress",
	"dbPass": "yeopress"
}
```

For a full example, open up the local `.yeopress` file that is created by the generator.  This file is located in the directory you ran `yo wordpress` in.

## Installing WordPress Plugins

New with `v1.4.0` is a subgenerator for installing plugins, `yo wordpress:plugin`.  You can supply a comma delimited list of plugin slugs to download.  YeoPress will download and unzip those plugins into your content directory.

### Visual Learner??

[Watch the video](http://www.youtube.com/watch?v=Em-NMCgNhhY).

ADD Visual Learner?  [Watch the shorter video](http://www.youtube.com/watch?v=WSG0P5VpSUk).

[Also see the wiki](https://github.com/wesleytodd/YeoPress/wiki)

[And here is the boring write-up...](http://wesleytodd.com/2013/5/yeopress-a-yeoman-generator-for-wordpress.html)

## Themes

Custom themes can be installed from GitHub or a Tarball.  Once installed, they are responsible for their own Gruntfile and related tasks.  A basic example template can be found in the [template branch](https://github.com/wesleytodd/YeoPress/tree/template) of this repo.  The example template comes with a few grunt tasks pre-configured:

- Regarde ([grunt-regarde](https://npmjs.org/package/grunt-regarde))
- Live Reload ([grunt-contrib-livereload](https://npmjs.org/package/grunt-contrib-livereload))
- Sass ([grunt-contrib-sass](https://npmjs.org/package/grunt-contrib-sass))
- JSHint ([grunt-contrib-jshint](https://npmjs.org/package/grunt-contrib-jshint))
- Bower ([grunt-bower-requirejs](https://npmjs.org/package/grunt-bower-requirejs))
- RequireJS ([grunt-contrib-requirejs](https://npmjs.org/package/grunt-contrib-requirejs))

More information on themes [here](https://github.com/wesleytodd/YeoPress/wiki/Themes) & [here](http://wesleytodd.com/2013/5/yeopress-themes.html)


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/wesleytodd/yeopress/trend.png)](https://bitdeli.com/free "Bitdeli Badge")



