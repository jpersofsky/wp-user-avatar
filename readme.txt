=== WP User Avatar ===

Contributors: bangbay
Donate link: http://siboliban.org/donate
Tags: author image, author photo, author avatar, avatar, profile avatar, profile image, profile photo, user avatar, user image, user photo
Requires at least: 3.3
Tested up to: 3.5.1
Stable tag: 1.2
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Use any image in your WordPress Media Library as a custom user avatar. Add your own Default Avatar.

== Description ==

WordPress currently only allows you to use custom avatars that are uploaded through [gravatar.com](http://gravatar.com/). WP User Avatar enables you to use any photo uploaded into your Media Library as an avatar. This means you use the same uploader and library as your posts. No extra folders or image editing functions are necessary.

To use WP User Avatar, choose a theme that has avatar support. In your theme, manually replace <code>get_avatar</code> with <code>get_wp_user_avatar</code> or leave <code>get_avatar</code> as-is. <code>get_wp_user_avatar</code> has functionality not available in <code>get_avatar</code>. [Read about the differences here](http://wordpress.org/extend/plugins/wp-user-avatar/faq/).

WP User Avatar also lets you:

* Upload your own Default Avatar in your Discussion settings.
* Show the user's gravatar.com avatar or Default Avatar if the user doesn't have a WP User Avatar image.
* Use the shortcode <code>[avatar]</code> in your posts. The shortcode will work with any theme, whether it has avatar support or not.

[Read more about get_avatar in the WordPress Function Reference](http://codex.wordpress.org/Function_Reference/get_avatar).

This plugin uses the Media uploader introduced in WordPress 3.5, but is also backwards-compatible to WordPress 3.3.

== Installation ==

1. Download, install, and activate the WP User Avatar plugin.
2. On your edit profile page, click "Edit WP User Avatar".
3. Choose an image, then click "Set WP User Avatar".
4. Click "Update Profile".
5. Upload your own Default Avatar in your Discussion settings (optional).
6. Choose a theme that has avatar support. In your theme, manually replace <code>get_avatar</code> with <code>get_wp_user_avatar</code> or leave <code>get_avatar</code> as-is. [Read about the differences here](http://wordpress.org/extend/plugins/wp-user-avatar/faq/).
7. You can also use the shortcode <code>[avatar]</code> in your posts. The shortcode will work with any theme, whether it has avatar support or not.

**Example Usage**

Within The Loop, you may be using:

`<?php echo get_avatar(get_the_author_meta('ID'), 96); ?>`

Replace this function with:

`<?php echo get_wp_user_avatar(get_the_author_meta('ID'), 96); ?>`

You can also use the values "original", "large", "medium", or "thumbnail" for your avatar size:

`<?php echo get_wp_user_avatar(get_the_author_meta('ID'), 'medium'); ?>`

You can also add an alignment of "left", "right", or "center":

`<?php echo get_wp_user_avatar(get_the_author_meta('ID'), 96, 'left'); ?>`

On an author page outside of The Loop, you may be using:

`<?php
  $user = get_user_by('slug', $author_name); 
  echo get_avatar($user->ID, 96);
?>`

Replace this function with:

`<?php
  $user = get_user_by('slug', $author_name);
  echo get_wp_user_avatar($user->ID, 96);
?>`

If you leave the options blank, WP User Avatar will detect whether you're inside The Loop or on an author page and return the correct avatar in the default 96x96 size:

`<?php echo get_wp_user_avatar(); ?>`

The function <code>get_wp_user_avatar</code> will also fall back to <code>get_avatar</code> if no WP User Avatar image is set. For this to work, "Show Avatars" must be checked in your Discussion settings. When this setting is enabled, you will see the user's gravatar.com avatar or Default Avatar.

**Other Available Functions**

= [avatar] shortcode =

You can use the shortcode <code>[avatar]</code> in your posts. It will detect the author of the post or you can specify an author by username. You can specify a size and alignment, but they are optional.

`[avatar user="admin" size="medium" align="left"]`

= get_wp_user_avatar_src =

Works just like <code>get_wp_user_avatar</code> but returns just the image src. This is useful if you would like to link a thumbnail-sized avatar to a larger version of the image:

`<a href="<?php echo get_wp_user_avatar_src($user_id, 'large'); ?>">
  <?php echo get_wp_user_avatar($user_id, 'thumbnail'); ?>
</a>`

= has_wp_user_avatar =

Returns true if the user has a WP User Avatar image. You can specify the user ID, or leave it blank to detect the author within The Loop or author page:

`<?php
  if ( has_wp_user_avatar($user_id) ) {
    echo get_wp_user_avatar($user_id, 96);
  } else {
    echo '<img src="my-alternate-image.jpg" />';
  }
?>`

== Frequently Asked Questions ==

= How do I use WP User Avatar? =

First, choose a theme that has avatar support. In your theme, you have a choice of manually replacing <code>get_avatar</code> with <code>get_wp_user_avatar</code>, or leaving <code>get_avatar</code> as-is. Here are the differences:

= get_wp_user_avatar =

1. Allows you to use the values "original", "large", "medium", or "thumbnail" for your avatar size.
2. Doesn't add a fixed width and height to the image if you use the aforementioned values. This will give you more flexibility to resize the image with CSS.
3. Optionally adds CSS classes "alignleft", "alignright", or "aligncenter" to position your avatar.
4. Shows nothing if the user has no WP User Avatar image.
5. Shows the user's gravatar.com avatar or the Default Avatar only if "Show Avatars" is enabled in your Discussion settings.

= get_avatar =

1. Requires you to enable "Show Avatars" in your Discussion settings to show any avatars.
2. Accepts only numeric values for your avatar size.
3. Always adds a fixed width and height to your image. This may cause problems if you use responsive CSS in your theme.
4. Show the user's gravatar.com avatar or the Default Avatar if the user doesn't have a WP User Avatar image. (Choosing "Blank" as your Default Avatar still generates a transparent image file.)
5. Requires no changes to your theme files if you are currently using <code>get_avatar</code>.

= Can I create a custom Default Avatar? =
In your Discussion settings, you can upload your own Default Avatar.

= Can I insert WP User Avatar directly into a post? =

You can use the shortcode <code>[avatar]</code> in your posts. The shortcode will work with any theme, whether it has avatar support or not. It will detect the author of the post or you can specify an author by username. You can specify a size or alignment, but they are optional.

`[avatar user="admin" size="medium" align="left"]`

= Will WP User Avatar work with comment author avatars? =

Yes, for registered users. Non-registered comment authors will show their gravatar.com avatars.

= How can I see which users have an avatar? =

For administrators, WP User Avatar adds a column with avatar thumbnails to your Users admin table. If "Show Avatars" is enabled in your Discussion settings, you will see avatars to the left of each username instead of in a new column.

= What CSS can I use with WP User Avatar? =

WP User Avatar will add the CSS classes "wp-user-avatar" and "wp-user-avatar-{size}" to your image. If you add an alignment, the corresponding alignment class will be added:

`<?php echo get_wp_user_avatar($user_id, 96, 'left'); ?>`

Outputs:

`<img src="{imageURL}" width="96" height="96" class="wp-user-avatar wp-user-avatar-96 alignleft" />`

If you use the values "original", "large", "medium", or "thumbnail", no width or height will be added to the image. This will give you more flexibility to resize the image with CSS:

`<?php echo get_wp_user_avatar($user_id, 'medium'); ?>`

Outputs:

`<img src="{imageURL}" class="wp-user-avatar wp-user-avatar-medium" />`

**Note:** WordPress adds more CSS classes to the avatar not listed here.

= What other functions are available for WP User Avatar? =
* <code>get_wp_user_avatar_src</code> - retrieve just the image URL
* <code>has_wp_user_avatar</code> - check if the user has a WP User Avatar image

[See example usage here](http://wordpress.org/extend/plugins/wp-user-avatar/installation/)

== Screenshots ==

1. WP User Avatar lets you upload your own Default Avatar.
2. WP User Avatar adds a field to your profile in edit mode.
3. After you've set a WP User Avatar image, you will see the option to remove it.

== Changelog ==

= 1.2 =
* Add: Default Avatar setting

= 1.1.7 =
* Bug Fix: Change update_usermeta to update_user_meta

= 1.1.6 =
* Bug Fix: Image not showing in user profile edit

= 1.1.5a =
* Update: readme.txt

= 1.1.5 =
* Bug Fix: Remove stray curly bracket

= 1.1.4 =
* Bug Fix: Change get_usermeta to get_user_meta
* Bug Fix: Non-object warning when retrieving user ID

= 1.1.3 =
* Bug Fix: Comment author with no e-mail address

= 1.1.2 =
* Remove: Unused variables

= 1.1.1 =
* Bug Fix: Capabilities error in comment avatar

= 1.1 =
* Add: Add filter for get_avatar
* Add: CSS alignment classes
* Add: Replace comment author avatar
* Add: Shortcode
* Update: readme.txt

= 1.0.2 =
* Update: FAQ
* Remove: CSS that hides "Insert into Post"

= 1.0.1 =
* Add: CSS classes to image output

= 1.0 =
* Initial release

== Upgrade Notice ==

= 1.2=
* New Feature: Default Avatar customization

= 1.1 =
* New Features: [avatar] shortcode, direct replacement of get_avatar() and comment author avatar, more CSS classes
