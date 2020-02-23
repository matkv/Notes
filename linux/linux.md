# Linux

[ArchWiki](https://wiki.archlinux.org/index.php/Main_page)

## Manjaro Linux

### Pamac

Pamac is an easier to use package manager than Manjaro's default one called Octopi. In its preferences, in the AUR tab, we can easily **enable the AUR repository**. Once it is installed, Octopi can be removed by selecting all the Octopi packages in Pamac and right clicking -> Remove.

### Installing & enabling a firewall

Manjaro does not have a graphical utility installed for the firewall. To install one, we open pamac and search for gufw package and install it. In order to be able to run it in our desktop environment (KDE Plasma for example), we need to edit the /bin/gufw file.

```bash
sudo nano /bin/gufw
```

Add this line (Ctrl+O to save, Ctrl+X to close):

```bash
kdesu python3 /usr/lib/python3.7/site-packages/gufw/gufw.py
```

Then we can open the GUI program for the firewall. For most users, just enabling the Firewall is enough.

### Enabling trim for SSD's

TRIM is a program that helps to clean blocks in your SSD and use it more efficiently and extend the SSD’s life. To enable TRIM on Manjaro, run the following command in a terminal:

```bash
sudo systemctl enable fstrim.timer
```

### Removing Orphans (Unused) packages

When we install and remove different packages, sometimes there are some packages which remain on our system but they are not used by any program. They are the **Orphan** packages. To save space on our hard drive, it’s a good idea to uninstall them.

In Pamac under the installed section, we can access the orphans section. Pamac will show all the orphan packages and we can remove them there.

### Backups

One of the easiest backup tools for Manjar is **Dèjá Dup Backup Tool**. Using this tool, it is possible to select which folders should be backed up, set up a shedule and even save them on Google Drive if desired.

### Creating a desktop application for any website using Nativefier

[Naitivefier Github repository](https://github.com/jiahaog/nativefier)

1. nativefier "www.website-link.com"
2. Navigate to the new created folder (for example website-link-linux-x64/)
3. sudo chown root chrome-sandbox
4. sudo chmod 4755 chrome-sandbox
5. The webapp can now be run by calling ./website-link 