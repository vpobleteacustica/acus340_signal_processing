# Configuración del entorno --- ACUS340

Esta guía describe los pasos necesarios para preparar el entorno de
trabajo del curso.

---

## Objetivo

Al finalizar estos pasos, deberías poder:

-   Usar Python con Anaconda/Miniconda
-   Ejecutar notebooks Jupyter
-   Utilizar Git y GitHub
-   Clonar el repositorio del curso

---

## 1. Verificar instalaciones

Abre una terminal y ejecuta:

conda --version\
python --version\
git --version

Si algún comando no funciona, debes instalarlo.

---

## 2. Instalación de herramientas

### Git

-   Mac (con Homebrew): brew install git

-   Windows: https://git-scm.com/downloads

---

### VS Code

https://code.visualstudio.com/

---

### Cuenta GitHub

https://github.com/

---

## 3. Configurar Git

git config --global user.name "Tu Nombre" git config --global user.email
"tu_correo@email.com"

---

## 4. Clonar repositorio del curso

git clone
https://github.com/vpobleteacustica/acus340_signal_processing.git\
cd acus340_signal_processing

---

## 5. Crear / activar entorno

Si el entorno no existe:

conda env create -f environment.yml

Activar entorno:

conda activate acus340_2026

---

## 6. Verificar librerías

python -c "import numpy, librosa, sklearn; print('OK')"

---

## 7. Instalar Jupyter

pip install jupyter ipykernel

Registrar entorno:

python -m ipykernel install --user --name acus340_2026 --display-name
"acus340_2026"

---

## 8. Ejecutar Jupyter

jupyter notebook

Abrir carpeta:

notebooks/

---

## 9. VS Code (opcional)

Abrir carpeta:

code .

Seleccionar entorno:

acus340_2026

---

## Problemas comunes

-   Conda no reconocido → reiniciar terminal
-   Git no instalado → instalar desde web
-   Jupyter no abre → instalar jupyter
-   Kernel no aparece → instalar ipykernel

---

## Resultado esperado

Deberías poder:

-   Abrir un notebook
-   Ejecutar código Python
-   Cargar librerías
-   Trabajar con el repositorio del curso

---

Curso ACUS340 --- Universidad Austral de Chile --- Instituto de Acústica
