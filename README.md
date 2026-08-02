# Guía de Personalización de KDE Plasma (CachyOS)

--- 

## **📌 Introducción**
Este documento es una guía completa para personalizar **KDE Plasma** en **CachyOS** (basado en Arch Linux) con un enfoque en:
- **Diseño tiling** (similar a Hyprland).
- **Personalización visual** (bordes verdes, blur, wallpapers por escritorio virtual).
- **Productividad y multitarea** (atajos de teclado, widgets, gestión de ventanas).
- **Instalación de software y drivers** para hardware espec铆fico.

--- 

## **📋 Requisitos Previos**
1. **Sistema base**: CachyOS instalado con KDE Plasma.
2. **Conexión a Internet** (para instalar paquetes).
3. **Permisos de administrador** (sudo).

--- 

## **🛠️ Instalación de Paquetes Básicos**

### **1. Actualizar el sistema**
```bash
sudo pacman -Syu
```

### **2. Instalar paquetes esenciales para personalización**

#### **Herramientas de personalización de KDE Plasma**
```bash
sudo pacman -S --needed \
    plasma \
    kde-applications \
    kwin \
    kwriteconfig5 \
    kwin-scripts \
    plasma6-applets-eventcalendar \
    plasma6-applets-window-title \
    plasma6-applets-window-buttons \
    plasma6-applets-thermal-monitor \
    plasma6-applets-system-monitor \
    plasma6-applets-weather-widget \
    plasma6-applets-blur \
    plasma6-themes-breath \
    plasma6-themes-sweet \
    plasma6-themes-arc \
    konsole \
    dolphin
```

#### **Herramientas para el modo tiling (KWin Scripts)**
```bash
sudo pacman -S --needed \
    kwin-script-bismuth \
    kwin-script-force-blur \
    kwin-script-window-title-in-window
```

#### **Selectores de wallpapers y utilidades**
```bash
yay -S --needed \
    skwd-wall \
    swww \
    hyprpaper
```

#### **Terminales personalizables**
```bash
sudo pacman -S --needed \
    alacritty \
    kitty
```

#### **Herramientas para widgets y monitoreo**
```bash
sudo pacman -S --needed \
    btop \
    waybar \
    eww
```

--- 

## **🎨 Personalización Visual**

### **1. Configuración de KWin para modo tiling**

#### **Habilitar el script Bismuth para tiling**
1. Abrir **Configuraci贸n de KWin**:
   ```bash
   kwin_wayland --replace &
   ```
2. Ir a **KWin Scripts** y activar **Bismuth**. 
3. Configurar atajos de teclado en **Bismuth Settings** (ejemplo: `Super + [1-9]` para cambiar de escritorio).

#### **Configuración de bordes verdes y blur**
1. Instalar el script **Force Blur** en KWin:
   - Descargar desde [KDE Store](https://store.kde.org/p/1305889/).
   - Activar en **KWin Scripts**. 
2. Configurar el color de borde:
   - Editar el archivo de configuración de KWin:
     ```bash
     nano ~/.config/kwinrc
     ```
   - Añadir o modificar:
     ```ini
     [Effect-ForceBlur]
     BorderColor=2,255,255,255,100  # Verde claro (RGBA)
     BlurStrength=10
     ```

### **2. Selector de wallpapers por escritorio virtual (skwd-wall)**

#### **Instalación y configuración**
1. Instalar `skwd-wall`:
   ```bash
   yay -S skwd-wall
   ```
2. Configurar `skwd-wall` para cambiar wallpapers por escritorio:
   - Crear un archivo de configuraci贸n:
     ```bash
     mkdir -p ~/.config/skwd
     nano ~/.config/skwd/config
     ```
   - Ejemplo de configuraci贸n:
     ```ini
     [General]
     WallpaperDir=/home/user/.local/share/wallpapers
     DefaultWallpaper=default.png
     
     [Desktop1]
     Wallpaper=wallpaper1.png
     
     [Desktop2]
     Wallpaper=wallpaper2.png
     ```
3. Ejecutar `skwd-wall` al inicio:
   - Añadir a **Autostart** de KDE:
     ```bash
     cp /usr/share/applications/skwd-wall.desktop ~/.config/autostart/
     ```

### **3. Barra lateral izquierda con flap**

## **Personalizar Barra KDE Plasma con Panel**

#### **Configuración de scrolling de escritorios visuales**
1. Usar **KWin Scripts** para scrolling:
   - Instalar **Desktop Cube** o **Overview Effect** desde KDE Store.
   - Configurar atajos de teclado para scrolling:
     ```bash
     kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --group Overview --key "Meta" "org.kde.kglobalaccel,/component/kwin,,invokeShortcut,string:Overview"
     ```

--- 

## **⌨️ Atajos de Teclado Personalizados**

### **1. Crear archivo de atajos de teclado**
1. Crear el archivo de configuración:
   ```bash
   mkdir -p ~/.config/khotkeys
   nano ~/.config/khotkeys/custom_shortcuts
   ```

2. Ejemplo de atajos (formato `.khotkeys`):
   ```ini
   [Shortcut1]
   Name=Terminal (Alacritty)
   Comment=Abrir terminal con Super + Enter
   Command=alacritty
   Shortcut=Meta+Return
   
   [Shortcut2]
   Name=Navegador (Brave)
   Comment=Abrir navegador con Super + Shift + B
   Command=brave
   Shortcut=Meta+Shift+B
   
   [Shortcut3]
   Name=Men煤 de Aplicaciones
   Comment=Abrir men煤 con Super + Space
   Command=krunner
   Shortcut=Meta+Space
   
   [Shortcut4]
   Name=Obsidian
   Comment=Abrir Obsidian con Super + O
   Command=obsidian
   Shortcut=Meta+O
   
   [Shortcut5]
   Name=Cambiar a Escritorio 1
   Comment=Super + 1
   Command=qdbus org.kde.kwin /KWin org.kde.KWin.setCurrentDesktop 1
   Shortcut=Meta+1
   
   [Shortcut6]
   Name=Cambiar a Escritorio 2
   Comment=Super + 2
   Command=qdbus org.kde.kwin /KWin org.kde.KWin.setCurrentDesktop 2
   Shortcut=Meta+2
   ```

3. Cargar los atajos en KDE:
   - Abrir **Configuración del Sistema > Atajos de Teclado > Personalizados**.
   - Importar el archivo `.khotkeys`.

--- 

## **📦 Lista de Software Adicional**

### **1. Software de Productividad y Desarrollo**

#### **Editores y IDEs**
```bash
sudo pacman -S --needed \
    obsidian \
    sublime-text \
    jetbrains-toolbox \
    code
```

#### **Herramientas de Desarrollo**
```bash
sudo pacman -S --needed \
    git \
    java-openjdk \
    nodejs \
    pnpm \
    go \
    kotlin \
    python \
    rust \
    docker
```

#### **Navegadores**
```bash
sudo pacman -S --needed \
    brave-browser \
    librewolf
```

### **2. Software Multimedia**

#### **Edición de Video y Audio**
```bash
sudo pacman -S --needed \
    davinci-resolve \
    obs-studio \
    audacity \
    kdenlive
```

#### **Reproductores de Música**
```bash
sudo pacman -S --needed \
    glassy-music-nankill \
    spotify-launcher \
    spicetify
```

### **3. Software de Comunicación**

#### **Mensajería y Videollamadas**
```bash
sudo pacman -S --needed \
    whatsapp-desktop \
    discord \
    zoom \
    microsoft-teams
```

#### **Correo Electrónico**
```bash
sudo pacman -S --needed \
    thunderbird
```

### **4. Software de Juegos**
```bash
sudo pacman -S --needed \
    steam \
    lutris \
    heroic-games-launcher \
    pcsx2 \
    wine \
    winetricks
```

### **5. Software de Nube Local**

#### **OneDrive y Google Drive**
```bash
yay -S --needed \
    onedriver \
    google-drive-ocamlfuse \
    rclone
```

#### **Microsoft 365 Business**
```bash
yay -S --needed \
    onlyoffice-desktopeditors
```

### **6. Software de Seguridad y VPN**
```bash
sudo pacman -S --needed \
    mullvad-vpn \
    nordvpn \
    bitwarden
```

### **7. Utilidades del Sistema**
```bash
sudo pacman -S --needed \
    btop \
    htop \
    neofetch \
    filelight \
    gparted \
    ark \
    okular
```

### **8. CLI Tools**
```bash
sudo pacman -S --needed \
    claude-cli \
    zsh \
    oh-my-zsh \
    fzf \
    ripgrep \
    bat
```

--- 

## **🔧 Instalación de Drivers**

### **1. Drivers para NVIDIA**
```bash
sudo pacman -S --needed \
    nvidia \
    nvidia-utils \
    nvidia-settings \
    lib32-nvidia-utils
```

### **2. Drivers para Bluetooth y USB**
```bash
sudo pacman -S --needed \
    bluez \
    bluez-utils \
    bluez-libs \
    usb_modeswitch
```

### **3. Drivers para Gamepads y Dispositivos de Entrada**
```bash
sudo pacman -S --needed \
    xpadneo \
    libratbag \
    solanum
```

### **4. Drivers para Webcam y Micrófono**
```bash
sudo pacman -S --needed \
    v4l-utils \
    ffmpeg \
    pulseaudio \
    pulseaudio-alsa \
    pavucontrol
```

### **5. Drivers para Ratón Logitech MX Master 3S**
```bash
sudo pacman -S --needed \
    libratbag \
    piper
```

### **6. Drivers para Teclado Royal Kludge**
- Verificar compatibilidad con `lsusb` y buscar drivers específicos si es necesario.
- Para teclados mecánicos, generalmente no se requieren drivers adicionales.

--- 

## **🎯 Configuración de Widgets y Capas**

### **1. Widgets con EWW (ElKowar's Wacky Widgets)**
1. Instalar `eww`:
   ```bash
   yay -S eww
   ```

2. Crear un archivo de configuración para widgets:
   ```bash
   mkdir -p ~/.config/eww
   nano ~/.config/eww/config.eww
   ```

3. Ejemplo de configuración para widgets:
   ```yaml
   # Configuraci贸n para widgets de volumen, CPU, temperatura, etc.
   
   def window : main {
       size: 300x600
       position: 100,100
       background: "#222222AA"
       border: 1
       border-color: "#00FF00"
   }
   
   def widget : volume {
       type: slider
       command: "pactl get-sink-volume @DEFAULT_SINK@ | awk '{print $5}' | tr -d '%'"
       on-change: "pactl set-sink-volume @DEFAULT_SINK@ +5%"
   }
   
   def widget : cpu {
       type: label
       command: "top -bn1 | grep 'Cpu(s)' | awk '{print $2 + $4}'"
       interval: 1
   }
   
   def widget : temperature {
       type: label
       command: "sensors | grep 'Package id' | awk '{print $4}' | tr -d '+掳C'"
       interval: 1
   }
   ```

4. Ejecutar `eww` al inicio:
   - Añadir a **Autostart** de KDE:
     ```bash
     cp /usr/share/applications/eww.desktop ~/.config/autostart/
     ```

### **2. Widgets con Waybar**
1. Instalar `waybar`:
   ```bash
   sudo pacman -S waybar
   ```

2. Configurar `waybar`:
   ```bash
   mkdir -p ~/.config/waybar
   nano ~/.config/waybar/config
   ```

3. Ejemplo de configuración:
   ```json
   {
       "layer": "top",
       "position": "left",
       "modules-left": ["menu", "workspaces"],
       "modules-center": ["window-title"],
       "modules-right": ["tray", "clock", "cpu", "memory", "temperature", "volume", "battery"],
       "menu": {
           "exec": "rofi -show drun"
       },
       "clock": {
           "format": "{:%Y-%m-%d %H:%M:%S}"
       },
       "cpu": {
           "format": "CPU: {}%",
           "interval": 1
       },
       "memory": {
           "format": "RAM: {}%",
           "interval": 1
       },
       "temperature": {
           "format": "TEMP: {}掳C",
           "interval": 1
       }
   }
   ```

--- 

## **📝 Configuración de Terminales**

### **1. Configuración de Alacritty**
1. Instalar `alacritty`:
   ```bash
   sudo pacman -S alacritty
   ```

2. Configurar `alacritty`:
   ```bash
   mkdir -p ~/.config/alacritty
   nano ~/.config/alacritty/alacritty.yml o alacritty.toml
   ```

3. Ejemplo de configuración:
   ```yaml
   window:
     padding:
       x: 10
       y: 10
     decorations: none
     opacity: 0.9
   
   font:
     normal:
       family: "Fira Code"
       style: "Regular"
     size: 12
   
   colors:
     primary:
       background: "#1E1E2E"
       foreground: "#CDD6F4"
     cursor:
       text: "#1E1E2E"
       cursor: "#F5E0DC"
     normal:
       black: "#45475A"
       red: "#F38BA8"
       green: "#A6E3A1"
       yellow: "#F9E2AF"
       blue: "#89B4FA"
       magenta: "#F5C2E7"
       cyan: "#94E2D5"
       white: "#BAC2DE"
   
   key_bindings:
     - { key: Return, mods: Super, action: Spawn(new_instance) }
     - { key: B, mods: Super|Shift, action: Spawn(command: { program: "brave" }) }
   ```

### **2. Configuración de Kitty**
1. Instalar `kitty`:
   ```bash
   sudo pacman -S kitty
   ```

2. Configurar `kitty`:
   ```bash
   mkdir -p ~/.config/kitty
   nano ~/.config/kitty/kitty.conf
   ```

3. Ejemplo de configuración:
   ```ini
   window_padding_width 10
   window_opacity 0.9
   
   font_family      Fira Code
   font_size        12
   
   background #1E1E2E
   foreground #CDD6F4
   cursor #F5E0DC
   cursor_text_color #1E1E2E
   
   url_color #89B4FA
   
   map super+enter launch alacritty
   map super+shift+b launch brave
   ```

--- 

## **🔄 Scripts de Automatización**

### **1. Script para aplicar configuraciones**
1. Crear un script para aplicar todas las configuraciones:
   ```bash
   nano ~/apply_kde_config.sh
   ```

2. Contenido del script:
   ```bash
   #!/bin/bash
   
   # Aplicar configuraciones de KWin
   cp -r ~/.config/kwinrc ~/.config/kwinrc.bak
   kwriteconfig5 --file kwinrc --group Effect-ForceBlur --group General --key BorderColor "2,255,255,255,100"
   kwriteconfig5 --file kwinrc --group Effect-ForceBlur --group General --key BlurStrength 10
   
   # Aplicar atajos de teclado
   cp ~/.config/khotkeys/custom_shortcuts ~/.config/khotkeys/custom_shortcuts.bak
   kbuildsycoca5
   
   # Reiniciar KWin para aplicar cambios
   kwin_wayland --replace &
   
   echo "Configuraciones aplicadas correctamente."
   ```

3. Dar permisos de ejecución:
   ```bash
   chmod +x ~/apply_kde_config.sh
   ```

--- 

## **📌 Lista Final de Software Recomendado**

| **Categor铆a**               | **Software**                          |
|----------------------------|---------------------------------------|
| **Navegadores**            | Brave, Librewolf                      |
| **Editores de Texto/IDE**   | Obsidian, Sublime Text, JetBrains Toolbox, VS Code |
| **Terminales**             | Alacritty, Kitty                      |
| **Multimedia**             | DaVinci Resolve, OBS Studio, Audacity, Kdenlive |
| **Música**                 | Glassy Music Nankill, Spotify Launcher |
| **Juegos**                 | Steam, Lutris, Heroic Games Launcher, PCSX2 |
| **Comunicación**           | WhatsApp Desktop, Discord, Zoom, Microsoft Teams |
| **Correo**                 | Thunderbird                          |
| **VPN**                    | Mullvad, NordVPN                      |
| **Gestión de Contraseñas** | Bitwarden                             |
| **Ofimática**              | OnlyOffice                           |
| **Nube Local**             | OneDriver, Google Drive Ocamlfuse, Rclone |
| **Desarrollo**             | Git, Java, Node.js, Go, Kotlin, Python, Rust, Docker |
| **Utilidades del Sistema** | btop, htop, neofetch, filelight, gparted, ark, okular |
| **CLI Tools**              | Claude CLI, zsh, oh-my-zsh, fzf, ripgrep, bat |

--- 

## **🔍 Solución de Problemas**

### **1. Problemas con NVIDIA y Wayland**
- Si hay problemas con NVIDIA en Wayland, probar con X11:
  ```bash
  sudo nano /etc/sddm.conf
  ```
  - Cambiar `Session=plasma-wayland` a `Session=plasma`.

### **2. Widgets no se muestran**
- Verificar que `eww` o `waybar` estén en ejecución:
  ```bash
  pkill eww && eww daemon
  pkill waybar && waybar &
  ```

### **3. Atajos de teclado no funcionan**
- Verificar que no haya conflictos con otros atajos:
  ```bash
  kcmshell5 khotkeys
  ```

--- 

## **📚 Recursos Adicionales**
- [KDE Store](https://store.kde.org/) (Temas, widgets y scripts para KDE).
- [Arch Wiki](https://wiki.archlinux.org/) (Documentación oficial de Arch Linux).
- [CachyOS Wiki](https://wiki.cachyos.org/) (Documentación específica de CachyOS).

--- 

## **🎉 Conclusión**
Con esta guía, tendrás un **KDE Plasma** altamente personalizado, con:
✅ **Diseño tiling** (similar a Hyprland).
✅ **Estilo visual único** (bordes verdes, blur, wallpapers por escritorio).
✅ **Productividad mejorada** (atajos de teclado, widgets, gestión de ventanas).
✅ **Soporte completo para hardware** (NVIDIA, Bluetooth, USB, etc.).

--- 
