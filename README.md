# pterodactyl_fastdl
Pterodactyl FastDL

#### THIS TUTORIAL WORKS ONLY FOR PTERODACTYL PANEL 1.1.1 and above! Earlier versions can not have 2 variables on the same line in a JSON file.

Add current virtual.conf to conf.d directory of a nginx daemon and edit the line 
```
server_name  example.website.ro;
```
with your currently running node **FQDN**.

This virtual.conf is configured to run as root under /var/lib/pterodactyl/volumes/ and list directories from here as default.


We will need to configure our egg to use a JSON file parser

```
{
    "csgo/cfg/server.cfg": {
        "parser": "file",
        "find": {
            "sv_downloadurl": "sv_downloadurl \"http://{{env.P_SERVER_LOCATION}}/{{env.P_SERVER_UUID}}/csgo/\"",
            "sv_allowdownload": "sv_allowdownload \"1\"",
            "sv_allowupload": "sv_allowupload \"0\""
        }
    }
}
```
**NOTE**: Please pay attention that the "sv_downloadurl" variable has a /csgo at the end, this can be configured on ANY running egg with your desired path.


![alt text](http://repository.btstelecom.ro/pterodactyl_images/Screenshot_15.png)

After that, we need to name our Locations as our FQDN(this was much easier for me to configure it as we have the description for locations who show our CPU names.

So, location list should contain in "Short Code" the FQDN address, let's say 'example.website.ro' or your domain.

Finally, restart your nginx and your server running with the edited egg. That's it.

Our **sv_downloadurl** will be like this
`http://example.website.ro/{{PTERODACTYL_UUID}}/csgo`

## Have fun!