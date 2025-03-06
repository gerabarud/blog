[[_TOC_]]

## ZSH configurado para kubectl

Para reinstalar **Oh My Zsh**, **Powerlevel10k**, y los plugins más usados, sigue estos pasos:

---

### **1. Instalar Zsh** (si lo desinstalaste antes)
- **Debian/Ubuntu**:
  ```sh
  sudo apt update && sudo apt install zsh -y
  ```
- **Arch Linux**:
  ```sh
  sudo pacman -S zsh
  ```
- **macOS (Homebrew)**:
  ```sh
  brew install zsh
  ```

Una vez instalado, cambia la shell predeterminada a Zsh:
```sh
chsh -s $(which zsh)
```
Luego, cierra sesión y vuelve a ingresar o ejecuta `zsh`.

---

### **2. Instalar Oh My Zsh**
```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Esto instalará Oh My Zsh en `~/.oh-my-zsh` y creará un archivo `~/.zshrc`.

---

### **3. Instalar Powerlevel10k**
```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
Ahora, edita `~/.zshrc` y cambia el tema a `powerlevel10k`:
```sh
ZSH_THEME="powerlevel10k/powerlevel10k"
```
Guarda los cambios y recarga la configuración:
```sh
source ~/.zshrc
```
Sigue el asistente de Powerlevel10k para configurarlo.

---

### **4. Instalar Plugins útiles**
Ejecuta:

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-completions
```

Ahora edita `~/.zshrc` y cambia la los plugins por:

```sh
plugins=(git z zsh-autosuggestions zsh-syntax-highlighting zsh-completions)
```
---
**1️⃣ `git`**  
Agrega alias y funciones útiles para `git`.  
**Ejemplo**:  
- `gst` → `git status`  
- `gco <branch>` → `git checkout <branch>`

---
**2️⃣ `z`**  
Permite navegar rápidamente entre directorios visitados.  
**Ejemplo**:  
- Escribe `z <parte-del-nombre-del-directorio>` para ir rápidamente a ese directorio.

---
**3️⃣ `zsh-autosuggestions`**  
Sugeiere comandos basados en lo que has escrito antes.  
**Ejemplo**:  
- Escribe `git co` y aparecerá una sugerencia como `git checkout <branch>`.

---
**4️⃣ `zsh-syntax-highlighting`**  
Resalta la sintaxis de los comandos mientras los escribes.  
**Ejemplo**:  
- Comandos válidos en verde, erróneos en rojo.

---
**5️⃣ `zsh-completions`**  
Extiende el autocompletado de comandos en `zsh`.  
**Ejemplo**:  
- Completa comandos adicionales como `git` o `docker` con más opciones.

Guarda y recarga la configuración:

```sh
source ~/.zshrc
```

---

### **5. (Opcional) Instalar fuentes Nerd Fonts para iconos en Powerlevel10k**
Si usas Powerlevel10k con iconos, instala las fuentes Nerd Fonts:

- **Debian/Ubuntu**:
  ```sh
  sudo apt install fonts-firacode -y
  ```
- **Arch Linux**:
  ```sh
  sudo pacman -S ttf-firacode-nerd
  ```
- **macOS (Homebrew)**:
  ```sh
  brew tap homebrew/cask-fonts
  brew install --cask font-fira-code-nerd-font
  ```

Después, configura la terminal para usar la fuente **FiraCode Nerd Font**.

Para configurar **FiraCode Nerd Font** en tu terminal y aprovechar las ligaduras de Powerlevel10k, sigue estos pasos según tu sistema operativo y terminal.

### **🔹 GNOME Terminal (Ubuntu y derivados)**
1. Abre la terminal y ve a **Preferencias**.
2. En el perfil activo, busca **Texto** o **Fuente personalizada**.
3. Activa la opción y selecciona **FiraCode Nerd Font**.
4. Guarda y cierra.

### **🔹 Konsole (KDE)**
1. Abre **Konsole** y ve a **Preferencias del perfil**.
2. Selecciona la pestaña **Avanzado**.
3. En **Fuente**, elige **FiraCode Nerd Font**.
4. Aplica los cambios.

### **🔹 Alacritty**
Edita el archivo de configuración (`~/.config/alacritty/alacritty.yml`):

```yaml
font:
  normal:
    family: "FiraCode Nerd Font"
    style: Regular
  bold:
    family: "FiraCode Nerd Font"
    style: Bold
  italic:
    family: "FiraCode Nerd Font"
    style: Italic
```

### **🔹 Windows Terminal**
1. Abre **Configuración** en Windows Terminal.
2. Edita el perfil y en la opción **Fuente**, elige **FiraCode Nerd Font**.

### **🔹 iTerm2 (macOS)**
1. Ve a **Preferencias** → **Perfiles** → **Texto**.
2. En **Fuente**, haz clic en **Cambiar** y selecciona **FiraCode Nerd Font**.

---

## **3. Verificar que los iconos y ligaduras funcionan**
Ejecuta:

```sh
echo "  λ →"
```

Si ves los caracteres correctamente, la configuración está lista. 