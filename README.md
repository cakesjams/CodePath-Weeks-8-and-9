# Project 7 - WordPress Pentesting

Time spent: **11** hours spent in total
##  Report



1.  Authenticated Cross-Site Scripting (XSS) via Media File Metadata
  - [ ] Summary:
    - Malicious script can be inserted via the media library's Metadata
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.3
  - [ ] GIF Walkthrough
    - <img src="1.gif">
  - [ ] Steps to recreate:
    - Upload a media item
    - Insert script into the title box for the Metadata
    - Set the media item to link to its attachment page
    - Post to see XSS
  - [ ] Affected source code:
    - https://github.com/WordPress/WordPress/commit/28f838ca3ee205b6f39cd2bf23eb4e5f52796bd7
    - Removed in WP 4.2.2
  - [ ] Reference:
    - https://www.nighttype.com/posts/wordpress-pentesting/

2. Authenticated Shortcode Tags Cross-Site Scripting (CVE-2015-5714)
  - [ ] Summary:
    -  WP-Core Shortcode tags can be mixed with HTML which bypasses sanitation and validation
    -  Version affected: 4.2
  	-	Fixed in: 4.2.5
  - [ ] GIF Walkthrough:
    - <img src="2.gif">
  - [ ] Steps to recreate:
    - Experiment quotes and put HTML inside of shortcodes
    ```
    [caption width='1' caption='<a href="' ">]</a><a href="onClick='alert(1)'">
    ```
    - View the post to get the XSS
  - [ ] Source code:
    - https://github.com/WordPress/WordPress/commit/f72b21af23da6b6d54208e5c1d65ececdaa109c8

3. Authenticated Stored Cross-Site Scripting via Image Filename (CVE-2016-7168)
  - Summary:
    -
    - Vulnerability type: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.10
  - [ ] GIF Walkthrough:
    - <img src="3.gif">
  - [ ] Steps to recreate:
    - Send an image with a malicious filename to the admin for upload or use in a post
      - Example: `zorua<img src=rekt onerror=alert(1)>.jpg`
    - Convince the admin to post the image including a link to the file attachment page
    - Publish the url to the attachment page which will execute the XSS.
  - [ ] Source code:
    - https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0
  - [ ] Reference:
    - https://sumofpwn.nl/advisory/2016/persistent_cross_site_scripting_vulnerability_in_wordpress_due_to_unsafe_processing_of_file_names.html
