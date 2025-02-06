## **1. Introducción**

Este tutorial explica cómo instalar y usar SPAdes, una herramienta de
ensamblaje de genomas, desde el Subsistema de Windows para Linux (WSL).
Está diseñado para personas sin experiencia en programación.

------------------------------------------------------------------------

## **2. Instalación de WSL**

1.  Abre **PowerShell** como administrador.

2.  Ejecuta el siguiente comando para instalar **WSL y Ubuntu**:

<!-- -->

    # Ejecuta este comando en tu terminal si no tienes WSL instalado:
    wsl --install

1.  Reinicia tu PC cuando se te solicite.

2.  Abre de nuevo WSL.

## **3. Instalación de dependencias en Ubuntu**

Dentro de WSL (Ubuntu), instala las herramientas necesarias para
compilar y usar SPAdes:

1.  Actualiza los repositorios:

<!-- -->

    sudo apt update

1.  Instala las herramientas necesarias:

<!-- -->

    sudo apt install -y git cmake make g++ python3

1.  Verifica que las herramientas estén instaladas:

<!-- -->

    git --version
    cmake --version
    make --version
    g++ --version
    python3 --version

## **4. Descargar SPAdes**

Clona el repositorio oficial de SPAdes desde GitHub:

    git clone https://github.com/ablab/spades.git
    cd spades

## **5. Compilar SPAdes**

1.  Crea un directorio para la compilación:

<!-- -->

    mkdir build
    cd build

1.  Configura el proyecto con CMake:

<!-- -->

    cmake ..

1.  Compila el código:

<!-- -->

    make -j$(nproc)

Esto utilizará todos los núcleos disponibles de tu CPU para acelerar la
compilación.

## **6. Ejecutar SPAdes**

**Con datos de prueba**  
1. Crea archivos de prueba:

    echo -e "@read1\nACGTACGTACGT\n+\nFFFFFFFFFFFF" > reads_1.fastq
    echo -e "@read2\nTGCATGCATGCA\n+\nFFFFFFFFFFFF" > reads_2.fastq

1.  Ejecuta SPAdes:

<!-- -->

    ./bin/spades.py --pe1-1 reads_1.fastq --pe1-2 reads_2.fastq -o test_output

**Con tus propios datos**  
1. Si tienes archivos FASTQ reales, reemplaza los nombres en el comando:

    ./bin/spades.py --pe1-1 your_reads_1.fastq --pe1-2 your_reads_2.fastq -o real_output

1.  Cambia your\_reads\_1.fastq y your\_reads\_2.fastq por los nombres
    de tus archivos.

## **7. Verificar los resultados**

Los ensamblajes se guardan en el directorio de salida (test\_output o
real\_output). El archivo principal es contigs.fasta. 1. Lista los
archivos generados:

    ls test_output

1.  Revisa el archivo de ensamblaje:

<!-- -->

    cat test_output/contigs.fasta

## **8. Consejos finales**

-   Si necesitas ejecutar SPAdes frecuentemente, agrega el binario al
    PATH:

<!-- -->

    echo 'export PATH=$PATH:~/spades/build/bin' >> ~/.bashrc
    source ~/.bashrc

-   Ahora puedes usar SPAdes desde cualquier ubicación:

<!-- -->

    spades.py --help

## **9. Recursos adicionales**

-   Github de SPAdes: <https://github.com/ablab/spades>
-   Mi página de Github: <https://github.com/marinartmonkey>
