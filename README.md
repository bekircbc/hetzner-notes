# Create Hetzner Server

- create a server
- username and password with email angekommen. --we will not use ths password..
- open your server

- RESCUE AKTIVIEREN AND RESET -- new password is ready for rescue..
- open your server - give your rescue root and password..

- in rescue mode write -- for install operating sytem image from hetzner..

          installimage

          choose Arc linux

- in blue editor page

          change HOSTNAME as yourhostname

          change UEFI##PART /ext4 all to PART /ext4 all

          F2 and F10

- wait until 15 step of Hetzner installimage finished..

          reboot

          login as root

# Terminal of your computer

- opennew terminal on your computer...

- deleting known hosts

          rm ~/.ssh/known_hosts

- creating new user

          ssh root@IPSERVER

          - logged in as root

          pacman -Syu
          pacman -S nano sudo

          for configuration :

          EDITOR=nano visudo

         #%wheel ALL=(ALL:ALL) NOPASSWD: ALL  --- delete #

          ctrl+O and X

          useradd -m -G wheel DEINUSERNAME
          passwd DEINUSERNAME
          reboot

- login with your new username and password on hetzner..

# open new terminal

-write to console -- dein computer

          cd ~/.ssh
          ls
          ssh-copy-id -i ~/.ssh/id_ed25519.pub username@ipserver

          give your password to add user

- login without password

          ssh username@ipserver

- write console

            sudo pacman -S nginx
            sudo pacman -S nodejs
            sudo pacman -S git
            sudo pacman -S caddy
            sudo pacman -S pm2
            sudo pacman -S npm

            sudo mkdir /var/www
            cd /var
            sudo chown username ./www
            (if not works) -- sudo chmod 777 ./www
            cd /var/www
            sudo mkdir projects
            cd projects
            mkdir deineprojectname
            git clone sshrepolink

- after permision denied for git clone, open new terminal on your computer..

- if you want to add ssh-key to your new server.. write on hetzner console

            ssh-keygen -t ed25519 -C "your git email adresse"

- write : id_ed25519 as key-name

           eval "$(ssh-agent -s)"
           ssh-add ~/.ssh/id_ed25519
           cat ~/.ssh/id_ed25519.pub

           cd /var/
           sudo chmod 777 ./www

- if you can not clone, check connection..

            ssh -T git@github.com
            ssh -vT git@github.com

- add this ssh key to github

## for starting frontend on caddy

              git clone ssh-repo-link
              npm i
              npm run build
              sudo nano /etc/caddy/Caddyfile

- copy to Caddyfile
  copy it for all domains
  change port for backend and file path for html

          test.nrdz.de {
          handle_path /api/* {
          reverse_proxy localhost:8324
          }
          root * /var/www/projects/hetzner-test/hetzner-test-fontend/dist
          file_server
         }

         ctrl+O and X

              sudo systemctl status caddy
              sudo systemctl enable caddy
              sudo systemctl start caddy
              sudo systemctl status caddy

- you must restart caddy after all "/etc/caddy/Caddyfile" changes..

## for starting backend on pm2

              git clone ssh-repo-link
              npm i
              npm run build
              sudo pacman -S pm2
              pm2 start server.js
              pm2 list
              pm2 log

              pm2 stop servername -- stopping
              pm2 delete servername -- deleting

- write this on browser for testing your api

              http://your-domain-name:port

---

Finished ..

- If you have questions about hetzner, feel free to contact..

---

### zoom settings for ubuntu.22

      sudo apt install ./zoom_amd64.deb

      sudo gedit /etc/gdm3/custom.conf
      echo $XDG_SESSION_TYPE
      sudo gedit /etc/gdm3/custom.conf
      sudo gedit /etc/environment
      sudo apt remove zoom
      sudo apt install zoom
      sudo gedit /etc/gdm3/custom.conf
      sudo gedit /etc/environment
