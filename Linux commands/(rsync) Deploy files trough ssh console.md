#shell #linux #CI/CD #rsync

This will synchronize between local directory and remote trough SSH and will ignore local `node_modules`
```
rsync -avz --exclude='node_modules' -e 'ssh -i ~/.ssh/id_rsa' ~/Local\ Sites/new-shero-website/app/public/wp-content/themes/access-wordpress-theme sherodes@sip4-10095.us-midwest-1.nxcli.net:~/new-site.shero.io/html/wp-content/themes/
```