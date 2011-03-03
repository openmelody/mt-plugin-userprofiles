User Profiles is a plugin for Melody that adds support for extensible public user profiles to a Melody powered blog or web site. This allows each user and commenter in your system to be given a dedicated URL on which you can display information about the contributions they have made, contributions like comments, entries and more. 

# Features

* Commenters can upload a profile image (any authenticated commenter, including Vox, OpenID, etc.)
* Authenticated commenters can edit basic profile info
* Authors and commenters have extended profiles.  Extended profiles come with 22 built-in fields (such as City, Country, Birthdate, About Me, etc.).
* Custom fields for extended profiles can be defined by system administrators
* Publish profile pages for each author and commenter, including profile images, basic and extended profile info, recent entries, and recent comments.
* Automatically import profile images (avatars) for all your existing users from Gravatar, MyBlogLog, Vox, Livejournal, and BlogCatalog.
* AJAX function auto-imports avatars in the background after new commenters login.

# How it Works

Authenticated commenters can edit their profiles and upload a profile image:

<img src="/images/userprofiles_addimage_up.png" />

Finally, the `<mt:AuthorImageURL>` and `<mt:CommenterImageURL>` tags can be used to display the user's profile image on your published blog pages (or use the core "userpic" tags in 4.1)

Profile images are stored as *Assets* within Movable Type.  This means that these images can also be used in other ways, such as inserting them into entries.  Movable Type will keep the full size image (cropped to square, if necessary) and create thumbnails when using the tags described below.  Each profile image is tagged with '@userpic'.

In addition, extended profiles can be edited, either from the admin interface, or by commenter via the "edit profile" link after they login.  User Profile pages are published automatically as static pages, which boosts performance for high traffic sites.

# Template Tags

## `<mt:AuthorImageURL>`

This displays the url to a thumbnail of the author's profile image.  There is one optional argument:

* *size* - the size in pixels of square thumbnail, default is 50 pixels (each side)

## `<mt:IfAuthorImage>`

This conditional tag displays its contents if the author has uploaded a profile image.

## `<mt:AuthorImageURL>`

This displays the url to a thumbnail of the commenter's profile image.  There is one optional argument:

* *size* - the size in pixels of square thumbnail, default is 50 pixels (each side)

## `<mt:IfCommenterImage>`

This conditional tag displays its contents if the commenter has a profile image. 

Note: if you posted a comment on your own blog (while signed in), your profile image will be displayed using this tag.

**Example:**

In your "Entry Metadata" template module, your could add the following:

    <mt:IfAuthorImage>
      <img src="<mt:AuthorImageURL size="50">" align="left" /> 
    </mt:IfAuthorImage>

This would display the author's profile image, *if* they have one in their profile.

Similarly, in your "Comment Detail" module, you could add:

    <mt:IfCommenterImage>
      <img src="<mt:CommenterImageURL size="50">" align="left" />
    </mt:IfCommenterImage>

## `<mt:AuthorProfileURL>`

This displays the url to the author's published profile page.

## `<mt:CommenterProfileURL>`

This displays the url to the commenter's published profile page.

## `<mt:EntryAuthorLink>`

This replaces the core tag of the same name.  Instead of linking to the author's URL, it will link to the author's profile page.

## `<mt:CommentAuthorLink>`

This replaces the core tag of the same name.  Instead of linking to the commenter's URL, it will link to the commenter's profile page.  If the commenter was not authenticated, it will link to the URL provided.

## `<mt:UserProfile>`

This tag is used to display extended profile information.  There is one required argument:

* *field* - the name of the field that you wish to display.  For built-in fields, valid values are birthdate, first_name, last_name, address, city, state, country, mobile_phone, land_phone, sex, marital_status, occupation, company, signature, about_me, activities, interests, music, tv_shows, movies, books, or quotes. For custom-defined fields, use the defined name of the field (more on custom fields below).  Note that for the built-in "birthdate" field, you can also specify a "date_format" argument that follows MT's date formats.

## `<mt:AuthorComments>`

This container tag, which is used on the default "User Profile" template, displays the comments from the author in context.  On the published User Profile page, this is used to display a list of recent comments by the user.

# Default Profile Templates

User Profiles comes with several default templates that are easy to install with the <a href="http://mt-hacks.com/templateinstaller.html">Template Installer</a> plugin.  The User Profile template set includes the following templates:

* **Javascript** - This a replacement for the core "Javascript" index template.  If you have customized your existing template, it will be backed up during the installation process.  The new version includes some new features for User Profiles.

* **Edit User Profile** - This template module is used to display the "edit profile" page that commenter's see when they click the "Edit Profile" link.  Note that this template also displays the image upload and the "edit extended profile" pages.  You can customize the user profile experience (and extended profile fields) bu editing this module.  Note: you should not rename this template module.

* **User Profile** (Pro only) - This template module is used to publish the User Profile pages.  Customize this template to change the way user profiles are displayed.  A special note about this template -- when you save it, it will automatically republish all user profile pages (no need to republish your site). Note: you should not rename this template module.

* **YUI Javascript** (Pro only) - This template module includes reference links to several Yahoo Javascript libraries.  This template should be included in the Header template for all feedback templates (Entry archives).  The auto-image-import AJAX function uses these libraries.  Note:  if you are already using the <a href="http://mt-hacks.com/ajaxcomments.html">Ajax Comments</a> plugin, then you already have this module, so you don't need to include it again.

# Requirements

* Melody 1.0 or greater
* Image::Magick perl module

# Installation

1. Download the zip file and upload the contents of the 'plugins' folder to the 'plugins' directory of your MT installation.

2. You should now see an Upgrade Screen for User Profiles.  For User Profiles Pro, the upgrade will add a new table for extended profiles and import profile images for existing users in your system.

3. Go to System Overview, then to Preferences > Plugins.  Then choose User Profiles, then Settings.  Entry the blog_id for profile images and templates, and the path for uploading profile images, then save.

4. Return to the User Profiles settings and click the "Install Templates" button.  The templates will be installed into the blog you chose in the previous step.

5. In your "Header" template, add the following before the &lt;/head> tag:
      
        <mt:If name="include_javascript">
          <script type="text/javascript" src="<mt:Link template="javascript">"></script>
        </mt:If>

    And (Pro only) after the line that reads `<mt:If name="entry_template">`, add:
         
        <mt:Include module="YUI Javascript">

    Then save your "Header" template.

6. Republish your Javascript template and Entry archives for the chosen blog.

7. Upload a profile image from your profile. (Tip: the quickest way to get to your profile is to click the "Hi Username!" link in the very top right of the page.)  Click the link to add a profile image and follow the steps as shown above.

8. Edit your extended profile by clicking "Extended Profile" from your profile page.

9. Edit your templates to display profile images, as described in the Template Tags section above.

# Customizing Extended Profiles and Adding Custom Fields

User of User Profiles Pro may want to customized the display of the fields or add custom fields to the profiles.  <a href="http://mt-hacks.com/20071201-customizing-extended-user-profile-fields.html" target="_blank">Click to read an in-depth article on how to customize Extended Profiles</a>.

# License

The User Profile plugin for Melody is licensed under the same terms as Perl itself. 

# Copyright

Copyright 2011, The Open Melody Software Group. All rights reserved.

# Acknowledgements 

The User Profiles Plugin was created and made possible by the fine work of Mark Carey, who kindly donated his work to the Open Melody Software Group and to the Melody community at large. Thank you Mark.
