Gulp workflow for Foundation 5
==============================

### A workflow solution for foundation5-gulp projects

![Class Gulp](http://rmdias.com/images/subdomains/gulpworkflow/gulp-logo.png)

> gulp.js - The streaming build system

## In this project we use:

* [Foundation 5](http://foundation.zurb.com/)
* [Gulp](https://www.npmjs.org/package/gulp)
* [Gulp - Compass](https://www.npmjs.org/package/gulp-compass)
* [Gulp - Concat](https://npmjs.org/package/gulp-concat)
* [Gulp - Connect](https://www.npmjs.org/package/gulp-connect)
* [Gulp - If](https://www.npmjs.org/package/gulp-if)
* [Gulp - Imagemin](https://npmjs.org/package/gulp-imagemin)
* [Gulp - Minify - Css](https://www.npmjs.org/package/gulp-minify-css)
* [Gulp - Minify - Html](https://npmjs.org/package/gulp-minify-html)
* [Gulp - Uglify](https://npmjs.org/package/gulp-uglify)
* [Gulp - Util](https://www.npmjs.org/package/gulp-util)
* [Gulp - Webserver](https://github.com/schickling/gulp-webserver)
* [imagemin-pngcrush](https://www.npmjs.org/package/imagemin-pngcrush)

## Setting up your workstation

You need to install the following on your workstation:

Install nodejs

<pre>
http://nodejs.org/
</pre>

Install Ruby. if you're on a Mac it's already installed. Not sure?

<pre>
  ruby --version
</pre>

  If you're on Windows
  
<pre>
  http://rubyinstaller.org/
</pre>
  
Grab a copy of Foundation 5

<pre>
  http://foundation.zurb.com/
</pre>
    
Clone this repository or download to the desktop

<pre>
  https://github.com/peterajones/gulp-workflow-for-foundation5
</pre>

## Instructions

1. Rename the Foundation 5 directory to reflect your project
2. Copy the following files and folders from this repo to your project directory root.

<pre>
.
|--gulfile.js
|--index.html
|--index.php
|--package.json
|--/img
|--/slick
</pre>

This will overwrite Foundation's index.html file, but that's OK. You need to do this to complete the installation instructions.

## Folder Structure

You should have a file structure in the root of your project folder that looks like this:

<pre>
.
|--/css
|--/img
|--/js
|--/slick
|--.gitignore
|--gulpfile.js
|--humans.txt
|--index.html
|--index.php
|--package.json
|--README.md
|--robots.txt
</pre>

## Getting started...

Open your project in a text editor like Sublime text. Navigate to the gulp file.js and follow the instructions at the top of the page.

If you go the text editor route, place you editor beside your browser for maximum effect and efficiency.

Open up the terminal (or command line prompt) and navigate to your project directory.
Run this command to install the dependencies: (You may need to add the sudo command on a Mac.)

<pre>
  [sudo] npm install
</pre>

This will install all dependencies in a directory called node_modules at root level.

Check for updates:

<pre>
  [sudo] npm-check-updates -u
</pre>

This will download any new dependencies and upgrade the 'package.json' file automatically.

    
## Building the development environment

This is where you will be doing your project development.

1. Run this command from the terminal to build the development environment:

<pre>
  gulp devSetUp
</pre>

This will create a ''builds' folder in the root directory and inside there will be a 
'development' directory which is where you will do your work.

2. Point your browser to:

<pre>
  http://localhost:8080
</pre>

The rest of the setup instructions should now appear in your browser. For the sake of clarity, I will continue the instructions here.

## Next steps...

Back in the command line, you will need to exit the currently running proccess by typing:

<pre>
  ctrl +C
</pre>
    
Then run

<pre>
  gulp dev
</pre>
    
  This will start the development server.

  Open this index.html file (not the index.html file in the root directory) in a text editor

<pre>
  ./builds/development/index.html
</pre>

  and make some changes to the h1 tag around line 25 and save the file.
  If you have your browser setup beside your text editor you will automatically see   your changes.

  Pretty cool, huh?
  
## Reduce calls to external files...

If you view the source code, you can see that we are making five calls to external files:

1.  css/normalize.css
2.  css/foundation.css
3.  js/vendor/modernizr.js
4.  js/vendor/jquery.js
5.  js/foundation.min.js

The modernizr.js file is not needed in all projects so I will leave it up to you whether or not to remove the call to modernizr in this file.

Lastly, I will set up a new gulp task to concatenate the two javascript files into a new, unique js file, thus reducing our calls to external files to three.

You will have to do two simple things in this file:
    
    builds/development/index.html
1. Remove one of the links to the two css files (top of page) and re-name the remaining link to point to css/app.css.
2. Remove one of the links to the two js files (bottom of page) and re-name the remaining link to point to js/app.js.

  Like I said before, its up to you what to do with the call to modernizr.js.
  
  Save your changes. You won't notice any difference in the browser, but what has   happened here is that the two css files have been merged into one file named  'app.css' and the two js files have been merged into one file named 'app.js'. Two   calls instead of four!
  
## CSS & JS overrides...

To make your life easier (so you don't have to mess with Foundation's CSS or the JS files), just create two new files called 'myCSS.css' and 'myJS.js' and put them in builds/development/css and builds/development/js respectively. Now you can tweak your project using these two new files as they will be appended to the app.css and app.js files.

Once you have done this, try adding this to your myCSS.css file. 

    body{
      background: rgba(0, 198, 255, 0.13);
    } 
Hit save and checkout the new background colour.

Just to prove that the myJS.js file will work as well, add

    function myFunction() {
      window.alert('This rocks');
    }; 
    
to that file. When you save the file, the browser will show an alert message when you click the button.You need to be in the browser for this.

To add your own styles and functionality, you only have to add it to these two files.

When we move to production, only the two app files will get imported and minified greatly reducing the size of the project.

## Moving to Production...

Now that you have modified your web site and are happy with the results, it is time to move it to the production environment. These are the files that you will deploy to the production server. The only files that we are going to move are the essential ones like the

    .html, .css, .js, .txt and the image assets.
    
These files will be minified, uglified or compressed as needed. The point is to make the smallest and fastest loading web site possible.

There is only one command to run to achieve this.

Back in the command line, quit the previous proccess if it is still running

    ctrl + C
    
and then type
    
    NODE_ENV=production gulp prod
and hit the enter key.

Once you run this command, all of the necessary files will be built to your builds/production/ directory (which doesn't even exist yet until you run this command!)

This workflow has started a new web server in builds/production. If you look at the source code you will see a minified version of the HTML. A quick look at the app.css or app.js files in your editor, you can verify that the same thing has happened. Good luck editing any of those files!

## So what's the Point?

The point is making your web site fast! Check out how big your
    
    builds/development/directory
    
 is, and compare it to your
 
    builds/production/directory
    
If you have followed all of these instructions you will see that the builds/development/ directory is ~ 1.1MB on disk compared to the builds/production/ directory which weighs in at ~ 328 KB on disk (340 KB if you included modernizer.js). That's a savings of more than 60% to the size of your site when it goes to the production server! of course your mileage will vary depending on the assets you add to the project, but the point is well made that you will save big time in the end.

## Summary

1. You have setup your workstation with global installs of GIT, NODE, RUBY (if on a widows box) and GULP. Optionally you can globally install SASS, COMPASS and BROWSERIFY, if you need them - links are in the README.md file.
2. You have installed the NPM dependencies by running npm install in the command line.
You have checked for any updates to the NPM dependencies by running npm-check-updates -u in the command line which downloaded any updates AND updated the package.json file.
3. You followed the instructions at the top of the gulpfile.js file and ran gulp devSetUp to create the development environment in builds/development/.
4. You altered the builds/development.index.html and saw your changes in livereload.
5. You reduced the number of calls to external files.
6. You added your own .css and .js files for adding your styles/functionality and overrides.
7.Lastly, you built the production environment where all of your files and images have been minified.

## Happy coding!

Now it's time to start working on your Foundation 5 project.

Use this file to start building your project:

    builds/development/index.html

Just a reminder:

To start your development web server to reflect the changes in your browser, go back to the terminal and type:

    gulp dev
    
If you like this, send me an email: peter at peter-jones.ca

Thanks!
<br>
<br>
<br>