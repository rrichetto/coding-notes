# Become a Wordpress Developer



## Section 2: Getting Started



### Development vs. Production Environment

**Dev Environment** - a private, separate copy of your site that only you can see. It contains your work-in-progress.

**Production Environment** - your real, public website that everyone can see. This is the "live" version.



### Your site files

**Overall Site Files**: Home directory (ryanrichetto) > Local Sites

**Wordpress Files**: Local Sites > [your website name] > app > public

**wp-content** - the most important folder

**Wordpress Themes** - wp-content > themes



## Section 3: First Coding Steps: PHP



### Creating a New Theme

1. Navigate to wp-content > themes

2. Create a new folder that contains the following files

   1. `index.php` 

   2. `style.css` - it *must* be named `style.css` - WP looks for this file to give details about the theme

      1. At the top `style.css`, open up a set of comments and add the following:

      ```css
      /*
        Theme Name: Fictional University
        Author: Ryan Richetto
        Version: 1.0
      */
      ```

   3. `screenshot.png` - this is the file WP uses for the preview (ideally it should be 1200w x 900h)



### Wordpress Functions

- Wordpress has it's own set of built-in functions that we can use. For example:
  - `bloginfo()` - gives us all sorts of information about our site (just privide an argument)
  - `bloginfo('name')` - prints the title of the website (found in settings > general)
  - `bloginfo('description')` - prints the tagline of the website



### PHP: Arrays

- to make an array: `$names = array('John', 'Brad', 'Bill');`
- to get the length of the array = `count($names);`



## Section 4: Wordpress Specific PHP

### The Wordpress Loop

```php+HTML
<?php 

  while(have_posts()) {
    the_post(); ?>
    <h2><?php the_title(); ?></h2>
    <?php the_content(); ?>
  <?php }

?>
```

- `have_posts()` - true for false depending if there are posts or not
- `the_post()` - gets all relevant information about the next post ready to use
- `the_title()` - the post title
- `the_content()` - the post content



Depending on the current URL, WP will look for different file names in your themes folder to control what you see. WP will revert to `index.php` as a default if `single.php` or `page.php` are not found.

- Homepage = `index.php`
- Single post - `single.php`
- Single page - `page.php`



### Header and Footer

- Header = `header.php`
- Footer = `footer.php`



To actually use the header and footer contents within our `index.php` file:

- `get_header();`
- `get_footer();`



To get your `style.css` to work on the front end:

1. In `header.php`, add `wp_head();` in the `<head>` tags. The `wp_head()` function lets WP control our head element.

```php+HTML
<!DOCTYPE html>

<html>
  <head>
    <?php wp_head(); ?>
  </head>
  <body>
    <h1>Fictional University</h1>
```

2. Make a `functions.php` file with the following:

```php+HTML
<?php

function university_files() {
  // (our nickname for stylesheet, location that points towards the file)
  wp_enqueue_style('university_main_styles', get_stylesheet_uri());
}

// (tell WP what/when we want to do something, name of our function we want WP to call)
add_action('wp_enqueue_scripts', 'university_files');
```

- `wp_enqueue_scripts` means you want to load some CSS or JS files



### Adding the WordPress Admin Bar

- In `footer.php`, before the closing `</body>` tag, you add `<?php wp_footer(); ?>`.



### Including Scripts and Stylesheets in functions.php

```php+HTML
<?php

function university_files() {
  wp_enqueue_script('main-university-js', get_theme_file_uri('/js/scripts-bundled.js'), NULL, microtime(), true);
  /*
  	NULL = this script does not depend on any other scripts
  	microtime() = version number
  	true = do you want to load this file just before closing body tag?
  */
  
  wp_enqueue_style('custom-google-fonts', '//fonts.googleapis.com/css?family=Roboto+Condensed:300,300i,400,400i,700,700i|Roboto:100,300,400,400i,700,700i');
  
  wp_enqueue_style('font-awesome', '//maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css');
  
  wp_enqueue_style('university_main_styles', get_stylesheet_uri(), NULL, microtime());
}

add_action('wp_enqueue_scripts', 'university_files');
```

- `microtime()` prevents caching during development mode



### Generate the path to you 'theme' folder so you can add images

- Use the WP function `get_theme_file_uri()`

```php+HTML
background-image: url(<?php echo get_theme_file_uri('/images/library-hero.jpg'); ?>);
```



## Section 5: Pages



### Adding the Page Title in the Tab

```php+HTML
function university_features() {
	add_theme_support('title-tag');
}

add_action('after_setup_theme', 'university_features');
```



### Adding links to other pages

- `site_url()` supplies the root URL of your current site. Then anything you add as an argument gets added onto the URL.

```php+HTML
<ul>
  <li><a href="<?php echo site_url('/about-us'); ?>">About Us</a></li>
</ul>
```



### Getting Page and Parent Page IDs

- This line of code gets the ID of the current page, and uses that to lookup the ID of it's parent page.

```php+HTML
<?php
	echo wp_get_post_parent_id(get_the_ID());
?>
```



### Why Echo?

- if a WP function begins with `get`, it does not `echo` anything for you, it simply returns a value for you to use.
- if a WP function begins with `the`, then WP will handle `echo`-ing and outputing to the page for you.



### Associative Array

- Associating a value with each array item

```php+HTML
<?php
$animalSounds = array(
              'cat' => 'meow',
              'dog' => 'bark',
              'pig' => 'oink'
            );

echo $animalSounds['dog'];
?>
```

