# SteamLink on Raspberry Pi 4

## Vorraussetzungen

1. Raspberry Pi Imager herunterladen: https://www.raspberrypi.org/software/
2. Bootbare microSD-Karte erstellen mit `Raspberry Pi OS 32-bit (Debian Version 11 Bullseye)`
3. Raspberry Pi per HDMI anschließen (HDMI-Port am nächsten zum USB-C-Port verwenden)
4. Ethernet-Kabel statt WLAN verwenden

## Setup
   
1. Konfiguration öffnen
```
sudo nano /boot/config.txt
```
2. Konfigurationswerte anpassen (Referenz: https://www.raspberrypi.org/documentation/computers/config_txt.html)
```
# Overscan (Schwarzen Rand um Bildschrim verhindern)
disable_overscan=1

# Maximale Taktfrequenz erhöhen
arm_freq=2000
over_voltage=6
gpu_freq=650

# Grafikspeicher
gpu_mem=512

```
3. Boot in Nicht-GUI-Umgebung aktivieren
```
sudo raspi-config
```
System Options --> Boot --> Boot to console with auto-login

3. Neustarten um Einstellungen anzuwenden

4. Installation von SteamLink
```
sudo apt install steamlink
```
5. Steamlink in Autostart aufnehmen
```
sudo nano /etc/systemd/system/steamlink.service
```
```
[Unit]
Description=SteamLink

[Service]
Type=simple
ExecStart=steamlink
Restart=on-failure
RestartSec=3

[Install]
WantedBy=default.target
```
```
sudo systemctl enable steamlink.service
```
