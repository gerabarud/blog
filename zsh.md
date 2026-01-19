[[_TOC_]]

# Kubernetes en la terminal: optimizando mi día a día con ZSH

Como administrador de distintos clusters de kubernetes y amante de la terminal, decidí optimizar mi flujo diario de trabajo. Para ello personalicé mi entorno con `zsh`, complementándolo con plugins y herramientas que me ayudan a trabajar más rápido y con menos fricción.

Les comparto mi un set-up inicial de la terminal `zsh` que te permite trabajar cómodo en la terminal y sin la necesidad de aplicaciones gráficas.

Mi entorno (puede replicarse en cualquier otro SO)
> UBUNTU 24.04

## **1. Instalar Zsh**
```sh
sudo apt update && sudo apt install zsh -y
```

Una vez instalado, cambia la shell predeterminada a `zsh`:
```sh
chsh -s $(which zsh)
```
Luego, cierra sesión y vuelve a ingresar o ejecuta `zsh`.

## **2. Instalar Oh My Zsh**
```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Esto instalará Oh My Zsh en `~/.oh-my-zsh` y creará un archivo `~/.zshrc`.

## **3. Instalar Powerlevel10k**
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

## **4. Instalar Plugins útiles**
Ejecuta:

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-completions
```

Ahora edita `~/.zshrc`, busca la variable `plugins` y agrega:

```sh
plugins=(kubectl git z zsh-autosuggestions zsh-syntax-highlighting zsh-completions fzf)
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

---

**6 `fzf` para lista seleccionable**

```bash
sudo apt install fzf                                                                         
```


Guarda y recarga la configuración:

```sh
source ~/.zshrc
```

## **5. Cambiar la shell predeterminada**

Para hacer zsh tu shell por defecto, usa:

```bash
chsh -s $(which zsh)
```
🔹 Esto cambiará la shell de tu usuario. Para que surta efecto, cierra sesión y vuelve a iniciar.

```bash
echo $SHELL
```
Si ves `/bin/zsh` o `/usr/bin/zsh`, ya está configurado correctamente.

---

## **6. (Opcional) Instalar fuentes Nerd Fonts para iconos en Powerlevel10k**
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

### **3. Verificar que los iconos y ligaduras funcionan**
Ejecuta:

```sh
echo "  λ →"
```

Si ves los caracteres correctamente, la configuración está lista. 

# `kubectl`

## **1. Instalar kubectl**

Actualice el índice de paquetes de apt e instale los paquetes necesarios para usar Kubernetes con el repositorio apt:
```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
```

Descargue la clave de firma pública de Google Cloud:
```bash
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
```

Agregue el repositorio de Kubernetes a apt:
```bash
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
 
Actualice el índice de paquetes de apt con el nuevo repositorio e instale kubectl:
```bash
sudo apt-get update
sudo apt-get install -y kubectl
```

## **2. Instalar krew**

Instalar
```bash
(
  set -x; cd "$(mktemp -d)" &&
  OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/arm.*$/arm/')" &&
  KREW="krew-${OS}_${ARCH}" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
  tar zxvf "${KREW}.tar.gz" &&
  ./"${KREW}" install krew
)
```

Agregarlo a al PATH
```bash
echo 'export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Instalar plugins con krew
```bash
kubectl krew install ns       # Alternativa a kubens
kubectl krew install ctx      # Alternativa a kubectx
kubectl krew install get-all  # Lista todos los recursos del cluster (usar con -n NS)
kubectl krew install stern
kubectl krew install tree
```

## **3. Activar autocompletado avanzado para `kubectl`**
Ejecuta este comando para generar el autocompletado de `kubectl`:  
```sh
kubectl completion zsh > ~/.kubectl-completion.sh
```
Ahora agrega esta línea a tu `.zshrc`:  
```sh
source ~/.kubectl-completion.sh
```
Y recarga la configuración:  
```sh
source ~/.zshrc
```

Esto habilita el autocompletado automático al escribir `kubectl`, sugiriendo nombres de recursos, namespaces, etc.

---

## **4. Instalar `kubectx` y `kubens` para cambiar de contexto rápido**
Si manejas múltiples clusters o namespaces, estos comandos te ahorrarán tiempo.

### **🔹 Instalación**
- **Debian/Ubuntu**:
  ```sh
  sudo apt install kubectx
  ```
- **Arch Linux**:
  ```sh
  sudo pacman -S kubectx
  ```
- **macOS (Homebrew)**:
  ```sh
  brew install kubectx
  ```

# **🔹 Alias útiles (agregar en `.zshrc`)**  

### **1️⃣ Monitorear Pods en tiempo real**
```sh
alias wkgp='watch -n 1 kubectl get pods -o wide'
```

---

### **2️⃣ Monitorear PVC en tiempor real**
```sh
alias wkgpvc='watch -n 1 kubectl get pvc'
```

---

### **3️⃣ Listar Pods con errores en todo el cluster**
> Lo ideal es que la lista esté vacía ;)
```sh
alias kgerror="kubectl get pods -A -o wide | grep -vi complete | grep -vi running"
```

---

### **4️⃣ Alias para kubectx y kubens**
```bash
alias kctx="kubectx"
alias kns="kubens"
```
---

### **5️⃣ Kubecolor**

Primero, instalarlo
```bash
curl -L https://github.com/dty1er/kubecolor/releases/latest/download/kubecolor-linux-amd64 -o /usr/local/bin/kubecolor
chmod +x /usr/local/bin/kubecolor
```

Alias:
```bash
alias kubectl="kubecolor"
```

---

### **6️⃣ Codificar un secreto en BASE64**
```sh
# Codificar en base64 con entrada interactiva
function b64enc() {
  echo -n "Texto a codificar: "
  read input
  echo -n "$input" | base64 -w 0  # En macOS usa `base64` sin `-w 0`
  echo
}
```

---

### **7️⃣ Decodificar un secreto en BASE64**
```sh
# Decodificar en base64 con entrada interactiva
function b64dec() {
  echo -n "Texto en base64: "
  read input
  echo "$input" | base64 -d  # En macOS usa `base64 -D`
  echo
}
```

### Aplicar cambios
```bash
source ~/.zshrc
```