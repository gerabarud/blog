## Paso 1: Instalación Completa de Paquetes y Dependencias

Ejecuta este comando unificado para instalar Sway, las utilidades multimedia, captura de pantalla, bloqueo de sesión, gestor de archivos y fuentes necesarias:

```bash
sudo apt update && sudo apt install -y \
    sway \
    swaylock \
    foot \
    wofi \
    wl-clipboard \
    cliphist \
    network-manager-gnome \
    playerctl \
    pulseaudio-utils \
    gnome-calculator \
    brightnessctl \
    grim \
    slurp \
    libnotify-bin \
    nautilus \
    python3 \
    curl \
    fonts-noto-color-emoji \
    fonts-font-awesome

```

---

## Paso 2: Creación de la Estructura de Directorios

Crea las carpetas de configuración en tu directorio personal:

```bash
mkdir -p ~/.config/sway ~/.config/foot

```

---

## Paso 3: Archivos de Configuración del Sistema

### 1. Archivo Principal de Sway (`~/.config/sway/config`)



Crea o edita el archivo `~/.config/sway/config` con todas las reglas de monitores, asignación de espacios de trabajo, teclas multimedia, reglas para Picture-in-Picture, capturas de pantalla y autostart:

```swayconfig
### Variables
set $mod Mod4
set $left h
set $down j
set $up k
set $right l
set $term env TERM=xterm-256color foot
set $menu wofi --show drun --prompt "Buscar aplicación..."

include /etc/sway/config-vars.d/*

### Configuración de Fondo de Pantalla
output * bg /home/gbarud/Imágenes/moon.png fill

### Configuración de Teclado
input type:keyboard {
    xkb_layout latam
    xkb_numlock enabled
}

### Atajos Básicos
bindsym $mod+Return exec $term
bindsym $mod+Shift+q kill
bindsym $mod+d exec $menu
floating_modifier $mod normal
bindsym $mod+Shift+c reload

### Navegación y Enfoque
bindsym $mod+$left focus left
bindsym $mod+$down focus down
bindsym $mod+$up focus up
bindsym $mod+$right focus right
bindsym $mod+Left focus left
bindsym $mod+Down focus down
bindsym $mod+Up focus up
bindsym $mod+Right focus right

### Mover Ventanas
bindsym $mod+Shift+$left move left
bindsym $mod+Shift+$down move down
bindsym $mod+Shift+$up move up
bindsym $mod+Shift+$right move right
bindsym $mod+Shift+Left move left
bindsym $mod+Shift+Down move down
bindsym $mod+Shift+Up move up
bindsym $mod+Shift+Right move right

### Workspaces
bindsym $mod+1 workspace number 1
bindsym $mod+2 workspace number 2
bindsym $mod+3 workspace number 3
bindsym $mod+4 workspace number 4
bindsym $mod+5 workspace number 5
bindsym $mod+6 workspace number 6
bindsym $mod+7 workspace number 7
bindsym $mod+8 workspace number 8
bindsym $mod+9 workspace number 9
bindsym $mod+0 workspace number 10

bindsym $mod+Shift+1 move container to workspace number 1
bindsym $mod+Shift+2 move container to workspace number 2
bindsym $mod+Shift+3 move container to workspace number 3
bindsym $mod+Shift+4 move container to workspace number 4
bindsym $mod+Shift+5 move container to workspace number 5
bindsym $mod+Shift+6 move container to workspace number 6
bindsym $mod+Shift+7 move container to workspace number 7
bindsym $mod+Shift+8 move container to workspace number 8
bindsym $mod+Shift+9 move container to workspace number 9
bindsym $mod+Shift+0 move container to workspace number 10

### Layouts
bindsym $mod+b splith
bindsym $mod+v splitv
bindsym $mod+s layout stacking
bindsym $mod+w layout tabbed
bindsym $mod+e layout toggle split
bindsym $mod+f fullscreen
bindsym $mod+Shift+space floating toggle
bindsym $mod+space focus mode_toggle
bindsym $mod+a focus parent

### Scratchpad
bindsym $mod+Shift+minus move scratchpad
bindsym $mod+minus scratchpad show

### Modo Redimensionar
mode "resize" {
    bindsym $left resize shrink width 10px
    bindsym $down resize grow height 10px
    bindsym $up resize shrink height 10px
    bindsym $right resize grow width 10px
    bindsym Left resize shrink width 10px
    bindsym Down resize grow height 10px
    bindsym Up resize shrink height 10px
    bindsym Right resize grow width 10px
    bindsym Return mode "default"
    bindsym Escape mode "default"
}
bindsym $mod+r mode "resize"

# =============================================================================
# 1. DEFINICIÓN DE VARIABLES
# =============================================================================
set $ws1 "1: Browsers"
set $ws2 "2: Terminales"
set $ws3 "3: VSCode"
set $ws4 "4: Archivos"

# =============================================================================
# 2. BARRAS DE ESTADO
# =============================================================================
bar {
    position top
    status_command ~/.config/sway/status.sh
    workspace_buttons no
    
    colors {
        statusline #ffffff
        background #1e1e1e
    }
}

bar {
    position bottom
    workspace_buttons yes
    tray_output *
    
    colors {
        statusline #ffffff
        background #1e1e1e
        active_workspace #4c78a0 #285577 #ffffff
        inactive_workspace #323232 #323232 #888888
    }
}

# =============================================================================
# 3. CONFIGURACIÓN DE PANTALLAS (MONITORES)
# =============================================================================
output HDMI-A-1 pos 0 0
output eDP-1 pos 1920 0

# =============================================================================
# 4. REGLAS DE ASIGNACIÓN (ASSIGN) Y DISEÑO (LAYOUT)
# =============================================================================
assign [app_id="firefox_firefox"] $ws1
assign [app_id="firefox"] $ws1
for_window [app_id="firefox_firefox"] layout stacking
for_window [app_id="firefox"] layout stacking

assign [app_id="chromium"] $ws1
assign [app_id="google-chrome"] $ws1
assign [class="Google-chrome"] $ws1
for_window [app_id="chromium"] layout stacking
for_window [app_id="google-chrome"] layout stacking
for_window [class="Google-chrome"] layout stacking

assign [app_id="foot"] $ws2

assign [class="code_code"] $ws3
assign [class="Code"] $ws3
for_window [class="code_code"] layout stacking
for_window [class="Code"] layout stacking

# Gestor de Archivos -> Workspace 4
assign [app_id="org.gnome.Nautilus"] $ws4
assign [class="Nautilus"] $ws4
assign [app_id="thunar"] $ws4

# =============================================================================
# 5. ATAJOS DE TECLADO PERSONALIZADOS
# =============================================================================
bindsym $mod+Control+Shift+Right move workspace to output right
bindsym $mod+Control+Shift+Left move workspace to output left
bindsym $mod+Control+Right focus output right
bindsym $mod+Control+Left focus output left

bindsym $mod+Shift+v exec cliphist list | wofi --dmenu --prompt "Historial..." | cliphist decode | wl-copy
bindsym $mod+t layout toggle stacking split

# Gestor de Red y VPN
bindsym $mod+n exec nm-connection-editor
for_window [app_id="nm-connection-editor"] floating enable

bindsym $mod+Shift+n exec foot --title="Gestor de Red" nmtui
for_window [title="Gestor de Red"] floating enable

# Menú de Apagado / Reinicio / Suspender / Cerrar Sesión
bindsym $mod+Shift+e exec ~/.config/sway/power-menu.sh

# Bloquear pantalla directamente
bindsym $mod+Control+l exec swaylock -f -c 000000

# =============================================================================
# 6. AUTOSTART Y SERVICIOS
# =============================================================================
exec dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP=sway
exec systemctl --user import-environment WAYLAND_DISPLAY XDG_CURRENT_DESKTOP

exec wl-paste --watch cliphist store
exec nm-applet --indicator

exec firefox
exec foot
exec code
exec nautilus

workspace $ws1

# =============================================================================
# 7. TECLAS MULTIMEDIA Y TECLAS ESPECIALES (XF86)
# =============================================================================
# Control de Volumen
bindsym --locked XF86AudioRaiseVolume exec pactl set-sink-volume @DEFAULT_SINK@ +5%
bindsym --locked XF86AudioLowerVolume exec pactl set-sink-volume @DEFAULT_SINK@ -5%
bindsym --locked XF86AudioMute exec pactl set-sink-mute @DEFAULT_SINK@ toggle
bindsym --locked XF86AudioMicMute exec pactl set-source-mute @DEFAULT_SOURCE@ toggle

# Control de Reproducción (Spotify, YouTube, Firefox, etc.)
bindsym --locked XF86AudioPlay exec playerctl play-pause
bindsym --locked XF86AudioNext exec playerctl next
bindsym --locked XF86AudioPrev exec playerctl previous

# Calculadora (se abre en modo flotante)
bindsym XF86Calculator exec gnome-calculator
for_window [app_id="org.gnome.Calculator"] floating enable
for_window [class="Gnome-calculator"] floating enable

# Brillo de pantalla (Laptops)
bindsym --locked XF86MonBrightnessUp exec brightnessctl set +5%
bindsym --locked XF86MonBrightnessDown exec brightnessctl set 5%-

# =============================================================================
# 8. REGLAS PARA PICTURE-IN-PICTURE (FLOTANTE + ADHESIVO)
# =============================================================================
for_window [title="(?i)picture-in-picture"] floating enable, sticky enable, resize set 640px 360px
for_window [title="Imagen en imagen"] floating enable, sticky enable, resize set 640px 360px
for_window [app_id="firefox" title="Picture-in-Picture"] floating enable, sticky enable, resize set 640px 360px

# =============================================================================
# 9. CAPTURAS DE PANTALLA (GRIM + SLURP)
# =============================================================================
bindsym Print exec grim - | wl-copy && notify-send "Captura de Pantalla" "Pantalla completa copiada al portapapeles"
bindsym Shift+Print exec grim -g "$(slurp)" - | wl-copy && notify-send "Captura de Pantalla" "Área copiada al portapapeles"
bindsym $mod+Print exec grim ~/Imágenes/captura_$(date +'%Y%m%d_%H%M%S').png && notify-send "Captura Guardada" "Guardada en ~/Imágenes"

```

---

### 2. Script de la Barra Superior (`~/.config/sway/status.sh`)



Crea el archivo `~/.config/sway/status.sh` para obtener información del sistema y clima:

```bash
#!/bin/bash

WEATHER_CACHE="/tmp/sway_weather"

while true; do
    # 1. Clima de alta precisión (Open-Meteo para San Juan, Argentina)
    if [ ! -f "$WEATHER_CACHE" ] || [ $(($(date +%s) - $(stat -c %Y "$WEATHER_CACHE" 2>/dev/null || echo 0))) -gt 600 ]; then
        (
            RES=$(python3 -c '
import urllib.request, json
try:
    url = "https://api.open-meteo.com/v1/forecast?latitude=-31.5375&longitude=-68.5364&current=temperature_2m,weather_code&timezone=auto"
    req = urllib.request.urlopen(url, timeout=4)
    data = json.loads(req.read().decode())
    temp = round(data["current"]["temperature_2m"])
    code = data["current"]["weather_code"]

    codes = {
        0: "☀️", 1: "🌤️", 2: "⛅", 3: "☁️",
        45: "🌫️", 48: "🌫️",
        51: "🌧️", 53: "🌧️", 55: "🌧️", 61: "🌧️", 63: "🌧️", 65: "🌧️",
        80: "🌦️", 81: "🌦️", 82: "🌧️",
        95: "⛈️️", 96: "⛈️", 99: "⛈️"
    }
    icon = codes.get(code, "🌡️")
    print(f"{icon} {temp}°C")
except Exception:
    print("N/A")
' 2>/dev/null)

            if [ -n "$RES" ] && [ "$RES" != "N/A" ]; then
                echo "$RES" > "$WEATHER_CACHE"
            fi
        ) &
    fi

    WEATHER=$(cat "$WEATHER_CACHE" 2>/dev/null)
    [ -z "$WEATHER" ] && WEATHER="N/A"

    # 2. RAM y CPU
    RAM=$(free -h | awk '/^Mem:/ {print $3 "/" $2}')
    CPU=$(top -bn1 | grep "%Cpu" | awk '{print $2 + $4 "%"}')

    # 3. Red
    ROUTE=$(ip route get 1.1.1.1 2>/dev/null)
    if [ -n "$ROUTE" ]; then
        IFACE=$(echo "$ROUTE" | awk '{print $5}')
        IP=$(echo "$ROUTE" | awk '{print $7}')

        if [[ "$IFACE" =~ ^(en|eth) ]]; then
            NET="Cable ($IP)"
        elif [[ "$IFACE" =~ ^wl ]]; then
            NET="WiFi ($IP)"
        else
            NET="$IFACE ($IP)"
        fi
    else
        NET="Sin conexión"
    fi

    # 4. Batería (si existe)
    BAT_INFO=""
    BAT_PATH=$(ls -d /sys/class/power_supply/BAT* 2>/dev/null | head -n1)
    if [ -n "$BAT_PATH" ] && [ -f "$BAT_PATH/capacity" ]; then
        CAP=$(cat "$BAT_PATH/capacity")
        STATUS=$(cat "$BAT_PATH/status")
        [ "$STATUS" = "Charging" ] && STAT_ICON="⚡" || STAT_ICON=""
        BAT_INFO=" | Bat: ${CAP}%${STAT_ICON}"
    fi

    # 5. Fecha
    DATE=$(LC_TIME=es_ES.UTF-8 date +"%d/%B/%Y - %H:%M")

    echo "RAM: $RAM | CPU: $CPU | Red: $NET$BAT_INFO | Clima: $WEATHER | $DATE"
    
    sleep 2
done

```

Otorga permisos de ejecución:

```bash
chmod +x ~/.config/sway/status.sh

```

---

### 3. Script del Menú de Apagado y Sistema (`~/.config/sway/power-menu.sh`)



Crea el archivo `~/.config/sway/power-menu.sh` para incluir las funciones de bloqueo, suspensión y apagado:

```bash
#!/bin/bash

OPCION=$(echo -e "1. 🔒 Bloquear Pantalla\n2. 🚪 Cerrar Sesión\n3. 🔄 Reiniciar\n4. ⚡ Apagar\n5. 🌙 Suspender" | wofi --dmenu --prompt "Sistema")

case "$OPCION" in
    *Bloquear*)
        swaylock -f -c 000000
        ;;
    *Cerrar*)
        swaymsg exit
        ;;
    *Reiniciar*)
        systemctl reboot
        ;;
    *Apagar*)
        systemctl poweroff
        ;;
    *Suspender*)
        systemctl suspend
        ;;
esac

```

Otorga permisos de ejecución:

```bash
chmod +x ~/.config/sway/power-menu.sh

```

---

### 4. Configuración de Foot (`~/.config/foot/foot.ini`)

Crea o edita `~/.config/foot/foot.ini`:

```ini
[main]
term=xterm-256color
font=monospace:size=14

```

---

## Paso 4: Definir Navegador Predeterminado

Ejecuta los siguientes comandos para enlazar Firefox como navegador predeterminado en el sistema:

```bash
xdg-settings set default-web-browser firefox.desktop
xdg-mime default firefox.desktop x-scheme-handler/http
xdg-mime default firefox.desktop x-scheme-handler/https
xdg-mime default firefox.desktop text/html
sudo update-alternatives --config x-www-browser

```

---

## Paso 5: Resumen de Atajos de Teclado Actualizado



| Combinación de Teclas | Acción / Función |
| --- | --- |
| **`Super` + `Enter**` | Abre la terminal `foot`. |
| **`Super` + `D**` | Abre el lanzador de aplicaciones `wofi`. |
| **`Super` + `Shift` + `Q**` | Cierra la ventana activa. |
| **`Super` + `T**` | Alterna la disposición entre **Mosaico (Split)** y **Pestañas Verticales (Stacking)**.

 |
| **`Super` + `E**` | Alterna la división de la ventana actual (`toggle split`).

 |
| **`Super` + `N**` | Abre el gestor gráfico de redes y VPN (`nm-connection-editor`) flotante.

 |
| **`Super` + `Shift` + `N**` | Abre la interfaz de red interactiva `nmtui` en una terminal flotante.

 |
| **`Super` + `Shift` + `V**` | Abre el menú del historial del portapapeles (`cliphist` + `wofi`).

 |
| **`Super` + `Shift` + `E**` | Despliega el menú del sistema (Bloquear, Cerrar Sesión, Reiniciar, Apagar, Suspender).

 |
| **`Super` + `Control` + `L**` | Bloquea la pantalla inmediatamente con `swaylock`.

 |
| **`Print Screen`** | Toma captura de pantalla completa y la copia al portapapeles.

 |
| **`Shift` + `Print Screen**` | Permite seleccionar un área con el ratón y copiar la captura al portapapeles.

 |
| **`Super` + `Print Screen**` | Guarda la captura de pantalla completa como archivo dentro de `~/Imágenes/`.

 |
| **`Teclas XF86 (Volumen/Brillo/Media)`** | Controla el volumen, el brillo de pantalla y la reproducción multimedia global.

 |
| **`Super` + `R**` | Entra al modo de redimensionar ventanas (*Resize*).

 |