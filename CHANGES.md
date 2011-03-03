# Change Log for the User Profiles Plugin for Melody

## 1.7

*Status: not ready yet.*

* Upgraded to use config.yaml.
* Converted docs to markdown and added to distro.
* Converted settings to config assistant.
* Updated license to Artistic, and Copyright to Open Melody Software Group.

## Movable Type Change Log

* 1.63 - fix for callback not firing when save Extended Profile - Thanks to Chad Everett for reporting this one
* 1.62 - fix for default Gravatar "G" icon being imported.
* 1.61 - another fix for XML::Parser error
* 1.6 - updated for MT 4.1, including migration to 4.1 "userpic" feature
* 1.53 - skip author/comment URL generation if blog_id not set (solves error after upgrade on dashboard).
* 1.52 - check for XML::Parser and skip those imports when not found, skip Profile build gracefully when no blog_id found
* 1.51 - bug fix for attempted profile build during initial install
* 1.5 - commenter upload of avatars + Pro version features
* 1.0 - orginal release of free version
