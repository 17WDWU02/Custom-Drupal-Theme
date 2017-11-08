# Custom-Drupal-Theme

## How to set up project for development


Before you start developing you want to set up drupal to be able to work in a development mode
Once you have created a new drupal project and the site has been built, then follow these sets

##### Go to sites/example.settings.local.php.
Take a copy of that file and move it into the default folder which is on the same directory, once copied over, remove the example from the file name. It should now be called **settings.local.php**
Open that file and go down to line **67**. Uncomment that line by remove the # at the beginning of the line.
This line will tell druapl to not cache every single file.
Remember you will still have to flush the cache everytime you create a new file.

---
##### Go to sites/default/settings.php.
Your line numbers might be different than mine but they should be in similar locations
Go down to line **710**. This section is abou trusted hosts. You need to include all the hosts which your website will be using.
Copy lines **723** to **725** and paste it at the end of the trusted host section which is around line **746** you will have to include all the hosts you use. It should look simiar to this
```php
 $settings['trusted_host_patterns'] = array(
    '^www\.example\.com$',
    '^192.168.33.10$',
    '^localhost$,
 );
```
If you IP address or URL is different then you will have to change it to suit your project. You will also have to edit it when you go live

Now scroll down to line **776**. This is near the end of the file, just above your database information.
You now need to tell drupal to register a new local settings file has been created.
Uncomment lines **787** to **789**
It should now look like this
```php
    if (file_exists($app_root . '/' . $site_path . '/settings.local.php')) {
        include $app_root . '/' . $site_path . '/settings.local.php';
    }
```

When you save this file it may ask for your password. It it does then go into finder and turn that one file to read and write privileges.

---
##### Go to sites/default/default.services.yml
Don't change any code in this file but rather use it as reference. Go to lin **39** and have a look at the twig.config section. At the moment everything in that section is turned off and the cache is true. We want to turn toggle those, but not in this file.
##### Go to sites/development.services.yml
Here is where we will change those settings from the other file. On line **5** is the paramerters section. In that section we need to include the twig.config section and toggle all of those settings. Remember to be cautious about your tabs or spaces as yml files read them differently than normal code.
Your paramaters section should now look like this
```yml
parameters:
  http.response.debug_cacheability_headers: true
  twig.config:
   debug: true
   auto_reload: true
   cache: false
```
---

Now all you need to do is flush the cache one last time and it should now work.
Check in your console to see if the twig comments have been added to the site.
Remember you still have to flush the cache every time a new file gets created in your project. But from then it should work perfectly fine.

If things arent working, either flush the cache, or go to /core/rebuild.php and see if that fixes the issue
