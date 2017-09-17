Rsync usage samples
===================
#### Linux local directories backup
Backup of Data disk dirs to Backup disk:
```bash
rsync -av --delete --exclude='desktop.ini' --exclude='Thumbs.db' \
  "/mnt/Data/Fred/My Videos/Videos_Famille" /mnt/Backup/DisqueSalon
rsync -av --delete --exclude='desktop.ini' --exclude='Thumbs.db' \
  "/mnt/Data/Fred/My Pictures/Photos" /mnt/Backup/DisqueSalon
```
