# AirCard para Linux 🎴

Personaliza el **diseño de las tarjetas de Apple Wallet** (y, de forma
experimental, el **teclado de la pantalla de bloqueo**) de un iPhone **sin
jailbreak**, directamente desde Linux. Se comunica con el iPhone por USB a
través de `usbmuxd` + `libimobiledevice`.

> Este repositorio es una **redistribución** del AppImage de
> [`kmw0410/AirCard-Linux`](https://github.com/kmw0410/AirCard-Linux) (licencia
> MIT), empaquetado junto a esta guía. El proyecto original es
> [`Mak5er/AirCard`](https://github.com/Mak5er/AirCard) (macOS) y
> [`Lumid-Off/AirCard-Windows`](https://github.com/Lumid-Off/AirCard-Windows).
> Todo el crédito es de sus autores. Ver [Licencia](#licencia) y [Créditos](#créditos).

---

## ✅ Qué funciona

| Función | Estado |
| :--- | :--- |
| **Cambiar la imagen de tarjetas de Wallet** (Apple Pay, tarjetas, pases) | ✅ Probado en iOS 27.2 |
| **Temas del teclado de desbloqueo** (`.passthm`, estilo Cowabunga/Nugget) | ⚠️ Experimental, sin verificar en dispositivo |

> La **Apple Card** usa render dinámico y no acepta skins estáticos. Sí funciona
> en tarjetas de débito/crédito normales, transporte y pases.

---

## 📋 Requisitos

- Linux **x86_64** con sesión gráfica (probado en **CachyOS**; otras distros sin verificar).
- Un **iPhone con iOS 18+** y su **cable USB**.
- Servicios/paquetes del sistema:
  - `usbmuxd` (servicio en ejecución)
  - `libimobiledevice` (aporta `idevice_id`, `ideviceinfo`, `idevicepair`)
  - `fuse2` (para ejecutar el AppImage)

### Instalar dependencias

**Arch / CachyOS:**
```bash
sudo pacman -S --needed usbmuxd libimobiledevice fuse2
sudo systemctl enable --now usbmuxd
```

**Debian / Ubuntu:**
```bash
sudo apt install usbmuxd libimobiledevice-utils libfuse2
sudo systemctl enable --now usbmuxd
```

**Fedora:**
```bash
sudo dnf install usbmuxd libimobiledevice-utils fuse-libs
sudo systemctl enable --now usbmuxd
```

---

## ⬇️ Descargar y ejecutar

**Descarga directa:** [AirCard-x86_64.AppImage (v0.1.2)](https://github.com/mclaider/aircard-linux/releases/latest/download/AirCard-x86_64.AppImage)
· [todas las versiones](https://github.com/mclaider/aircard-linux/releases)

```bash
curl -fLO https://github.com/mclaider/aircard-linux/releases/latest/download/AirCard-x86_64.AppImage
chmod +x AirCard-x86_64.AppImage
./AirCard-x86_64.AppImage
```

También está en el repo, en [`bin/AirCard-x86_64.AppImage`](bin/AirCard-x86_64.AppImage):

```bash
# Descargar este repo (o solo el AppImage)
git clone https://github.com/mclaider/aircard-linux.git
cd aircard-linux

# (opcional) verificar el checksum
sha256sum -c bin/AirCard-x86_64.AppImage.sha256

# Hacerlo ejecutable y lanzarlo
chmod +x bin/AirCard-x86_64.AppImage
./bin/AirCard-x86_64.AppImage
```

> **¿Error de FUSE?** (`libfuse.so.2 not found`) Ejecútalo así:
> ```bash
> ./bin/AirCard-x86_64.AppImage --appimage-extract-and-run
> ```

---

## 🚀 Cómo usarlo

1. **Conecta el iPhone** por USB y **desbloquéalo**.
2. Si es la primera vez, en el iPhone pulsa **"Confiar en este ordenador"** e
   introduce el código. (Comprobar desde terminal: `idevice_id -l` debe mostrar
   el UDID del iPhone.)
3. Abre AirCard. En **Device** debe aparecer tu iPhone.
4. Pulsa **Scan**.
5. En el iPhone abre **Wallet** y **toca la tarjeta** que quieres cambiar →
   AirCard captura su *hash* automáticamente.
6. Carga la **imagen** (PNG **1536 × 969 px** recomendado) y pulsa
   **Apply / Apply Artwork**.
7. En el iPhone: abre el **selector de apps**, **cierra Wallet** deslizándola y
   vuelve a abrirla → verás el nuevo diseño. (Si no, reinicia el iPhone.)

Arte gratuito para tarjetas: comunidad **[aircards.org](https://aircards.org/)**.

---

## 🛠️ Solución de problemas

- **No aparece el iPhone / `idevice_id -l` vacío:**
  ```bash
  sudo systemctl restart usbmuxd
  idevicepair pair     # con el iPhone desbloqueado
  idevice_id -l
  ```
  Prueba también a **desconectar y reconectar** el cable.
- **Emparejamiento:** `idevicepair pair` (desbloqueado) y acepta "Confiar" en el iPhone.
- **Info del dispositivo:** `ideviceinfo -k ProductVersion` (versión de iOS), `ideviceinfo -k DeviceName`.
- **No se ve el cambio:** fuerza el cierre de Wallet en el iPhone o reinícialo
  para que recargue la caché.

---

## ⚠️ Aviso

Herramienta de **personalización cosmética** de tu **propio** dispositivo. Úsala
bajo tu responsabilidad; puede dejar de funcionar si Apple cambia los mecanismos
internos. No requiere jailbreak. Sin garantía (ver licencia MIT).

---

## 📄 Licencia

**MIT** — ver [`LICENSE`](LICENSE). Se conserva el aviso de copyright de los
autores originales, como exige la licencia.

## 🙏 Créditos

- [`kmw0410/AirCard-Linux`](https://github.com/kmw0410/AirCard-Linux) — port a Linux (GTK/AppImage).
- [`Mak5er/AirCard`](https://github.com/Mak5er/AirCard) — proyecto original (macOS).
- [`Lumid-Off/AirCard-Windows`](https://github.com/Lumid-Off/AirCard-Windows) — port a Windows.
