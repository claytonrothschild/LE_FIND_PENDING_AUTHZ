# This is the only known working fork of LE_FIND_PENDING_AUTHZ IN 2021
I made quick edits to handle new authz-v3 endpoints and also handle changes to the JSON response objects that have been made since 2017. It can be refactored better, (for example, I did a simple .replace() to quickly remove a quote on an auth key), but it gets the job done for a problem most people wont need to even solve for.

## Usage:
The below readme is from (@sahsanu at LetsEncrypt Community Forums)[https://community.letsencrypt.org/t/too-many-requests-of-a-given-type-how-do-you-reset-this/44182/2]
```
cd /var/log/letsencrypt/
wget https://raw.githubusercontent.com/ahaw021/LE_FIND_PENDING_AUTHZ/master/LE_FIND_PENDING_AUTHZ.py
Edit python script LE_FIND_PENDING_AUTHZ.py and modify these 2 variables:
```

Before:

```
PATH = r""
KEY_FOLDER = r""
```

After (you need to use the right path to your account on key_folder variable):

```
PATH = r"/var/log/letsencrypt"
KEY_FOLDER = r"/etc/letsencrypt/accounts/acme-v01.api.letsencrypt.org/directory/xxxxxxxxxxxxxxxxxxxxxxxxx"
```

Save the file and execute it:

```
python LE_FIND_PENDING_AUTHZ.py
```

the script should invalidate the pending authzs (you should see something like this):

```
Reviewing Auth: 9lzHojU6yyT2vEzYuI0wnha1A3UR8eKObjiQJQdvkk0
         Status:pending Domain: yourdomain.tld  Expires: 2017-10-16T20:34:12Z
Invalidating :9lzHojU6yyT2vEzYuI0wnha1A3UR8eKObjiQJQdvkk0
and if you run the script again, the previous pending authz should be invalid now:

Reviewing Auth: 9lzHojU6yyT2vEzYuI0wnha1A3UR8eKObjiQJQdvkk0
         Status:invalid Domain: yourdomain.tld  Expires: 2017-10-16T20:34:12Z
If you have invalidated the pending authzs you should try to renew your certs again.
```
