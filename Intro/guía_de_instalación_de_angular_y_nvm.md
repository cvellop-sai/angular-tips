# Guía de Instalación de Angular CLI mediante NVM en Linux

Esta guía detalla el proceso paso a paso para preparar el entorno de desarrollo desde cero, instalando el gestor de versiones **NVM**, configurando **Node.js 22** e instalando la **CLI de Angular**.

---

## 1. Instalar NVM (Node Version Manager) en Linux

NVM permite gestionar múltiples versiones de Node.js en el mismo sistema sin problemas de permisos de superusuario (`sudo`).

### Pasos de instalación

1. Ejecuta el script oficial de instalación en la terminal:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

*(Si no tienes `curl` instalado, puedes usar `wget`)*:
```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

2. Carga la configuración de NVM en tu sesión actual de la terminal (o simplemente cierra y vuelve a abrir la terminal):

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

3. Comprueba que NVM se ha instalado correctamente:

```bash
nvm --version
```

---

## 2. Instalar y activar Node.js 22

Angular 22 requiere **Node.js v20.13.0+** o **v22.0.0+**. Con NVM podemos instalar y activar Node.js 22 fácilmente:

```bash
# Instalar la versión 22 de Node.js
nvm install 22

# Establecer la versión 22 como predeterminada y activa
nvm use 22
nvm alias default 22

# Verificar las versiones de Node.js y NPM
node -v
npm -v
```

---

## 3. Instalar Angular CLI (`ng`)

Una vez configurada la versión correcta de Node.js, procede a la instalación global del conjunto de herramientas de línea de comandos de Angular:

```bash
# Limpiar la caché de NPM para evitar conflictos previos
npm cache clean --force

# Instalar Angular CLI v22 globalmente
npm install -g @angular/cli@22
```

---

## 4. Verificar la instalación de Angular

Para comprobar que el comando `ng` está disponible y configurado con la versión correcta:

```bash
ng version
```

---

## 5. Crear y verificar un proyecto de prueba

Para comprobar que todo el entorno funciona de forma integrada:

```bash
# Crear un nuevo proyecto
ng new mi-proyecto-demo

# Acceder al directorio
cd mi-proyecto-demo

# Iniciar el servidor de desarrollo local
ng serve -o
```