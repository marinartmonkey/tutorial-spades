---
title: 'Tutorial SPAdes: ensamblaje de genomas desde WSL'
author: "Marina García Cervera"
date: "`r Sys.Date()`"
output:
  pdf_document:
    toc: true
    toc_depth: '2'
  html_document:
    toc: true
    toc_depth: 2
    toc_float:
      collapsed: false
      smooth_scroll: true
---

## **1. Introducción**
Este tutorial explica cómo instalar y usar SPAdes, una herramienta de ensamblaje de genomas, desde el Subsistema de Windows para Linux (WSL). Está diseñado para personas sin experiencia en programación.

---

## **2. Instalación de WSL**

1. Abre **PowerShell** como administrador.

2. Ejecuta el siguiente comando para instalar **WSL y Ubuntu**:

```{r, echo=TRUE, eval=FALSE}
# Ejecuta este comando en tu terminal si no tienes WSL instalado:
wsl --install
```

3. Reinicia tu PC cuando se te solicite.

4. Abre de nuevo WSL.

## **3. Instalación de dependencias en Ubuntu**
Dentro de WSL (Ubuntu), instala las herramientas necesarias para compilar y usar SPAdes:

1. Actualiza los repositorios:
```{r, echo=TRUE, eval=FALSE}
sudo apt update
```

2. Instala las herramientas necesarias:

```{r, echo=TRUE, eval=FALSE}
sudo apt install -y git cmake make g++ python3
```

3. Verifica que las herramientas estén instaladas:
```{r, echo=TRUE, eval=FALSE}
git --version
cmake --version
make --version
g++ --version
python3 --version
```

## **4. Descargar SPAdes**
Clona el repositorio oficial de SPAdes desde GitHub:
```{r, echo=TRUE, eval=FALSE}
git clone https://github.com/ablab/spades.git
cd spades
```

## **5. Compilar SPAdes**
1. Crea un directorio para la compilación:
```{r, echo=TRUE, eval=FALSE}
mkdir build
cd build
```

2. Configura el proyecto con CMake:
```{r, echo=TRUE, eval=FALSE}
cmake ..
```

3. Compila el código:
```{r, echo=TRUE, eval=FALSE}
make -j$(nproc)
```

Esto utilizará todos los núcleos disponibles de tu CPU para acelerar la compilación.

## **6. Ejecutar SPAdes**
**Con datos de prueba**  
1. Crea archivos de prueba:
```{r, echo=TRUE, eval=FALSE}
echo -e "@read1\nACGTACGTACGT\n+\nFFFFFFFFFFFF" > reads_1.fastq
echo -e "@read2\nTGCATGCATGCA\n+\nFFFFFFFFFFFF" > reads_2.fastq
```

2. Ejecuta SPAdes:
```{r, echo=TRUE, eval=FALSE}
./bin/spades.py --pe1-1 reads_1.fastq --pe1-2 reads_2.fastq -o test_output
```

**Con tus propios datos**  
1. Si tienes archivos FASTQ reales, reemplaza los nombres en el comando:
```{r, echo=TRUE, eval=FALSE}
./bin/spades.py --pe1-1 your_reads_1.fastq --pe1-2 your_reads_2.fastq -o real_output
```

2. Cambia your_reads_1.fastq y your_reads_2.fastq por los nombres de tus archivos.

## **7. Verificar los resultados** 
Los ensamblajes se guardan en el directorio de salida (test_output o real_output). El archivo principal es contigs.fasta.
1. Lista los archivos generados:
```{r, echo=TRUE, eval=FALSE}
ls test_output
```

2. Revisa el archivo de ensamblaje:
```{r, echo=TRUE, eval=FALSE}
cat test_output/contigs.fasta
```

## **8. Consejos finales** 
- Si necesitas ejecutar SPAdes frecuentemente, agrega el binario al PATH:
```{r, echo=TRUE, eval=FALSE}
echo 'export PATH=$PATH:~/spades/build/bin' >> ~/.bashrc
source ~/.bashrc
```
- Ahora puedes usar SPAdes desde cualquier ubicación:
```{r, echo=TRUE, eval=FALSE}
spades.py --help
```

## **9. Recursos adicionales**
- Github de SPAdes: https://github.com/ablab/spades
- Mi página de Github: https://github.com/marinartmonkey
