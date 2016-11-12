# Collection of changes necessary after a fresh Wordpress installation

created by Uwe (2016-04-05)

## Secure login by htaccess protection

A lot of attacs against wordpress installations are using the login
page and login using a stolen or guessed password or using a security
vulnerability. It become a good practice to protect the admin pages
of wordpress installations by a second barrier called htaccess.

### 1. Create a password file

```bash
htpasswd -c /path/to/the/wordpress/directory/.htpasswd jukey
```

### (optional) Change password

Thefollowing command changes the password for the user jukey:

```bash
htpasswd /path/to/the/wordpress/directory/.htpasswd jukey
```

### 2. Edit .htaccess

The htaccess file already contains the default entries that look like
this:

```
# BEGIN WordPress
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>

# END WordPress
```

Add the following below:

```
# BEGIN jukey
<Files wp-login.php>
 AuthName "Admin-Bereich"
 AuthType Basic
 AuthUserFile /path/to/the/.htpasswd
 require valid-user
</Files>

<FilesMatch "(\.htaccess|\.htpasswd|wp-config\.php|liesmich\.html|readme\.html)">
 order deny,allow
 deny from all
</FilesMatch>
# END jukey
```

# Edit wp-config.php


## Enable upload for files without restriction

Add the following at the end of the editable part of the config file:

```php
/* Edit by Uwe */
define("ALLOW_UNFILTERED_UPLOADS", true);

/* Das war’s, Schluss mit dem Bearbeiten! Viel Spaß beim Bloggen. */
/* That's all, stop editing! Happy blogging. */
```

# Export and Import

Could be found in the tools section
