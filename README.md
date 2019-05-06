# Lincoln Notes

Contact Kevin Becker for more info

## Working with Zendesk Custom Theme (basic method)

### Install Ruby

1. Go to https://rubyinstaller.org/downloads/ and download WITHOUT DEVKIT > Ruby 2.3.3 (x64) and install
2. Download DEVELOPMENT KIT (OLD) For use with Ruby 2.0 to 2.3 (x64 - 64bits only): DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe
3. Extract to C:/RubyDevKit/
4. Open "Start Command Prompt with Ruby" (installed in step 1)
5. CD to C:/RubyDevKit/
6. Run `ruby dk.rb init` and then `ruby dk.rb install` (https://github.com/oneclick/rubyinstaller/wiki/Development-Kit)
7. Note that you may need to add ruby to your PATH

### Install SassC
1. Run `gem install sassc`

### Developing
1. Work with the scss files for styles, not the css file

### Updating Theme in Zendesk
1. When done updating, go into manifest.json and increment the version number (Zendesk will throw an error if you try to pull an updated theme with the same version number)
2. CD into your project and run ruby ./bin/compile.rb to compile the sass into css
3. Commit & push your updated files included the manifest.json, scss files, css file, etc.
4. In Zendesk guide under themes find this theme (currently called "Custom Theme") click the 3 vertical dots and select Update from Github

---

## Working with Zendesk Custom Theme (advanced method: Windows 7 VM)
### Note: This method does not currently work correctly do to some authentication problems

### Install Ruby as above

### Install ZAT

1. Run `gem install rake` (https://develop.zendesk.com/hc/en-us/articles/360001075048)
2. Run `gem update zendesk_apps_tools`

### Setting env variable
1. Download certificate: https://curl.haxx.se/ca/cacert.pem
2. Put it somewhere permanent (I added to C:/RubyDevKit/)
3. In explorer right click This PC > Properties > Advanced System Settings > Environment Variables...
4. Under User variables select New... add Variable Name: SSL_CERT_FILE Variable Value: C:\RubyDevKit\cacert.pem or the path you added the file to above

### Running
1. CD to the project directory
2. Run `zat theme preview`
3. Enter https://lincolninvestment.zendesk.com/
4. Enter lincoln email and password
5. Get an error because either some settings/permissions in Zendesk need to be updated or OneLogin integration is breaking this.

---

# Copenhagen Theme by Zendesk

The Copenhagen theme is the default Zendesk Guide theme. It is designed to be responsive and accessible.
Learn more about customizing Zendesk Guide [here](https://support.zendesk.com/hc/en-us/sections/206670747).

The Copenhagen theme for Help Center consists of a [set of templates](#templates), [styles](#styles), a Javascript file used mainly for interactions and an [assets folder](#assets).

## How to use
This is the latest version of the Copenhagen theme available for Guide. It is possible to use this repository as a starting point to build your own custom theme. You can fork this repository as you see fit.
You can use your favorite IDE to develop themes and preview your changes locally in a web browser using the Zendesk Apps Tools (ZAT). For details, see [Previewing theme changes locally](https://support.zendesk.com/hc/en-us/articles/115014810447).

## Customizing your theme
Once you have forked this repository you can feel free to edit templates, CSS in `style.css` (if you would like to use SASS go to the [Using SASS section](#using-sass)), javascript and manage assets.

### Manifest file
The manifest allows you to define a group of settings for your theme that can then be changed via the UI in Theming Center.
You can read more about the manifest file [here](https://support.zendesk.com/hc/en-us/articles/115012547687).

### Settings folder
If you have a variable of type file, you need to provide a default file for that variable in the `/settings` folder. This file will be used on the settings panel by default and users can upload a different file if they like.
Ex.
If you would like to have a variable for the background image of a section, the variable in your manifest file would look something like this:

```js
{
  ...
  "settings": [{
    "label": "Images",
    "variables": [{
      "identifier": "background_image",
      "type": "file",
      "description": "Background image for X section",
      "label": "Background image",
    }]
  }]
}

```

And this would look for a file inside the settings folder named: `background_image`

### Adding assets
You can add assets to the asset folder and use them in your CSS, Javascript and templates.
You can read more about assets [here](https://support.zendesk.com/hc/en-us/articles/115012399428)


## Publishing your theme
After you have customized your theme you can download the repository as a `zip` file and import it into Theming Center.

You can follow the documentation for importing [here](https://support.zendesk.com/hc/en-us/articles/115012794168).

You can also import directly from GitHub - learn more [here](https://support.zendesk.com/hc/en-us/community/posts/360004400007).

## Templates
The theme includes all the templates that are used for a Help Center that has *all* the features available.
List of templates in the theme:
* Article page
* Category page
* Community post list page
* Community post page
* Community topic list page
* Community topic page
* Contributions page
* Document head
* Error page
* Footer
* Header
* Home page
* New community post page
* New request page
* Requests page
* Search results page
* Section page
* Subscriptions page
* User profile page

You can add up to 10 optional templates for:
 * Article page
 * Category page
 * Section page

You do this by creating files under the folders `templates/article_pages`, `templates/category_pages` or `templates/section_pages`.
Learn more [here](https://support.zendesk.com/hc/en-us/articles/360001948367).

## Styles
The styles that Theming Center needs to use in the theme are in the `style.css` file in the root folder.

The styles for the theme are split using Sass partials, all the partials are under [styles/](/blob/master/styles/), they are all included in the "main" file [index.scss](/blob/master/styles/index.scss) and then compiled to CSS.
If you wish to use SASS you can go to the [using SASS section](#using-sass)

## Assets
These are the images that are needed for the theme.
These include:
* Loader
* Dropdown arrow

# Using SASS
In order to use SASS for development, you just need to compile it into the CSS that Zendesk Guide understands.
Note: Zendesk App Tools [theme preview](#publishing-your-theme) currently does not support live SASS compilation.

## Requirements

- Install Ruby, we use `sassc` gem to compile our `.scss` files. You can see how to install Ruby [here](https://www.ruby-lang.org/en/documentation/installation/).
- Install `sassc` gem. You can run:
```
    gem install sassc
```

Now you can compile your SASS files running:
```
./bin/compile.rb
```
Which will take all the `scss` files inside the `styles/` folder and create the `style.css` file that is consumable by Zendesk Guide.

# Contributing
Bug reports and pull requests are welcome on GitHub at https://github.com/zendesk/copenhagen_theme
Please mention @zendesk/guide-growth when creating a bug report or a pull request.
