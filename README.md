# 🧬 Elementos de la sintaxis de Shell Scripting III

## 📚 Información del Curso
**Curso:** Principios de programación - Bioinformática  
**Universidad:** Universidad Peruana de Ciencias Aplicadas (UPC)  
**Programa:** Biología  
**Facultad:** Ciencias de la Salud  
**Semestre:** 2025-02  

### 👨‍🏫 Docentes:
- **Frank Guzman Escudero**
- **Manuel Ramírez Sáenz**

---

## 🎯 Objetivo de Aprendizaje

Al finalizar esta sesión, serás capaz de:

- ✅ **Usar bucles `while` y `for`** para automatizar tareas repetitivas
- ✅ **Implementar estructuras condicionales** (if, then, else, elif)
- ✅ **Trabajar con operadores de comparación** numéricos, texto y archivos
- ✅ **Aplicar estos conceptos** a análisis bioinformáticos
- ✅ **Automatizar procesamiento** de archivos y datos biológicos

**Palabras clave:** Bucles, while, for, if-then-else, comparaciones, bioinformática

---

## 📑 Contenido de la Clase

1. [Bucles WHILE](#-bucles-while)
2. [Operadores de Comparación](#-operadores-de-comparación)
3. [Estructuras Condicionales](#-estructuras-condicionales)
4. [Comando test](#-comando-test)
5. [Combinando FOR + IF](#-combinando-for--if)
6. [Ejemplos Bioinformáticos](#-ejemplos-bioinformáticos)
7. [Actividad Asincrónica - Misión Imposible](#-actividad-asincrónica---misión-imposible)

---

## 🔄 Bucles WHILE

### ¿Qué es un bucle WHILE?
Un bucle `while` ejecuta un conjunto de comandos repetidamente mientras una condición específica sea **verdadera**.

### 📝 Sintaxis básica

```bash
while [ CONDICIÓN ]
do
    comando1
    comando2
    comandoN
done
```

### 🔢 Ejemplo básico

```bash
#!/bin/bash
# Archivo: while.sh
number=10
while [ $number -gt 5 ]
do
    echo $number 
    number=$(($number-1))
done
```

**Resultado:**
```
10
9
8
7
6
```

### 🔄 Bucle infinito (¡Ten cuidado!)

```bash
#!/bin/bash
# Archivo: forever.sh
while [ true ]
do
    echo "Este es un bucle infinito. Presiona CTRL + C para salir."
    sleep 0.5
done
```

---

## 📊 Operadores de Comparación

### Para valores numéricos

| Operador | Significado |
|----------|-------------|
| `-lt` | Menor que (<) |
| `-gt` | Mayor que (>) |
| `-le` | Menor o igual que (≤) |
| `-ge` | Mayor o igual que (≥) |
| `-eq` | Igual (=) |
| `-ne` | No igual (≠) |

### Para texto/cadenas

| Operador | Significado |
|----------|-------------|
| `=` | Las cadenas son idénticas |
| `!=` | Las cadenas no son idénticas |
| `<` | Es menor que (alfabéticamente) |
| `>` | Es mayor que (alfabéticamente) |
| `-n` | La cadena no está vacía |
| `-z` | La cadena está vacía |

### Para archivos

| Operador | Significado |
|----------|-------------|
| `-e archivo` | El archivo existe |
| `-f archivo` | Es un archivo normal (no directorio) |
| `-d archivo` | Es un directorio |
| `-s archivo` | Tiene tamaño mayor que cero |
| `-r archivo` | Tiene permiso de lectura |
| `-w archivo` | Tiene permiso de escritura |
| `-x archivo` | Tiene permiso de ejecución |

---

## 🧠 Estructuras Condicionales

### IF simple

```bash
if [ condición ]
then
    comando1
    comando2
fi
```

### IF-ELSE

```bash
if [ condición ]
then
    comando1  # si se cumple la condición
else
    comando2  # si NO se cumple la condición
fi
```

### IF-ELIF-ELSE

```bash
if [ condición1 ]
then
    comando1  # si se cumple condición1
elif [ condición2 ]
then
    comando2  # si se cumple condición2
else
    comando3  # si no se cumple ninguna
fi
```

### 📝 Ejemplo práctico

```bash
#!/bin/bash
# Archivo: numeros.sh
num1=$1
num2=$2

if [ $num1 -gt $num2 ]; then
    echo "$num1 es mayor que $num2"
elif [ $num1 -lt $num2 ]; then
    echo "$num1 es menor que $num2"
else
    echo "$num1 es igual a $num2"
fi
```

**Uso:** `bash numeros.sh 10 5`

---

## 🔧 Comando test

El comando `test` evalúa expresiones y devuelve:
- **0** = Verdadero (éxito)
- **1** = Falso (no éxito)

### Formas de usar test

```bash
# Forma 1: Usando test explícitamente
test 3 -gt 1; echo "$?"

# Forma 2: Usando corchetes [ ]
[ 3 -gt 1 ]; echo "$?"
```

### Operadores lógicos

```bash
# Operador Y (&&): ejecuta comando2 solo si comando1 es exitoso
comando1 && comando2

# Operador O (||): ejecuta comando2 solo si comando1 falla
comando1 || comando2
```

### Ejemplo con operadores lógicos

```bash
#!/bin/bash
[ $1 -eq $2 ] && echo "$1=$2"
[ $1 -ne $2 ] && echo "$1!=$2"
[ $1 -lt $2 ] && echo "$1<$2"
[ $1 -gt $2 ] && echo "$1>$2"
```

---

## 🔄 Combinando FOR + IF

Puedes usar bucles `for` con estructuras `if` para aplicar condiciones a cada elemento:

```bash
#!/bin/bash
# Archivo: directorios.sh
for file in $(ls)
do
    if [ -d "$file" ]; then
        echo "directorio: $file"
    elif [ -x "$file" ]; then
        echo "archivo ejecutable: $file"
    else
        echo "archivo no ejecutable: $file"
    fi
done
```

---

## 🧬 Ejemplos Bioinformáticos

### 1. Contar secuencias en archivo FASTA

```bash
#!/bin/bash
# Archivo: clock1.sh
file="clock.fasta"
count=0

while IFS= read -r line
do
    if [[ $line == ">"* ]]; then
        ((count++))
    fi
done < "$file"

echo "Número de secuencias en $file: $count"
```

### 2. Verificar existencia de archivos

```bash
#!/bin/bash
archivo="/ruta/al/archivo.txt"

if [ -e "$archivo" ]; then
    echo "El archivo $archivo existe."
else
    echo "El archivo $archivo no existe o no es accesible."
fi
```

### 3. Consultar genes metilados

```bash
#!/bin/bash
# Archivo: metilados.sh
genes_metilados=("BRCA1" "MLH1" "CREBBP")

echo "Ingrese el nombre del gen que desea consultar:"
read gen

encontrado=false
for gene in "${genes_metilados[@]}"; do
    if [ "$gen" = "$gene" ]; then
        encontrado=true
        break
    fi
done

if [ "$encontrado" = true ]; then
    echo "El gen $gen está metilado y silenciado."
else
    echo "El gen $gen no está en la lista de genes metilados."
fi
```

### 4. Comparar secuencias de ADN

```bash
#!/bin/bash
# Archivo: secuencia.sh
secuencia1="ATCGATCG"
secuencia2="ATAGATCG"

if [ "$secuencia1" = "$secuencia2" ]; then
    echo "Las secuencias son idénticas"
else
    echo "Las secuencias son diferentes"
fi

if [ -n "$secuencia1" ]; then
    echo "La secuencia1 no está vacía"
fi

longitud1=${#secuencia1}
longitud2=${#secuencia2}
echo "Longitud de secuencia1: $longitud1"
echo "Longitud de secuencia2: $longitud2"
```

---

## 🎬 Actividad Asincrónica - MISIÓN IMPOSIBLE: OPERACIÓN BIOINFORMÁTICA

```
🎵 *Música de Misión Imposible sonando de fondo* 🎵
```

### 📼 MENSAJE SECRETO

```
Buenos días, Agente [TU NOMBRE].

Tu misión, si decides aceptarla, consiste en dominar las técnicas
avanzadas de control de flujo y estructuras condicionales en Shell
Scripting para análisis bioinformáticos.

Un laboratorio rival ha comprometido nuestros sistemas de análisis
y solo TÚ puedes restaurar la funcionalidad usando tus nuevas
habilidades con while, if-then-else y operadores de comparación.

Este mensaje se autodestruirá en 10 segundos... 💥

Buena suerte, Agente.
```

### 🎯 BRIEFING DE LA MISIÓN

#### 📋 **INFORMACIÓN CLASIFICADA:**
- **Código de Operación:** WHILE-IF-007
- **Nivel de Amenaza:** 🔴 CRÍTICO
- **Tiempo límite:** 7 días
- **Equipo requerido:** Terminal Linux/Mac o WSL en Windows
- **Armas secretas:** while, if-then-else, test, operadores de comparación

#### 🕵️ **TU IDENTIDAD ENCUBIERTA:**
- **Nombre en clave:** Agente Condicional
- **Especialidad:** Control de flujo y análisis automatizado
- **Misión:** Restaurar los sistemas de control de calidad genómica

---

### 🚨 MISIONES A COMPLETAR

#### 🧬 **MISIÓN 1: OPERACIÓN "SEQUENCE QUALITY CONTROL"**
**📍 Localización:** Laboratorio de Control de Calidad

Dr. Chaos ha alterado nuestro sistema de validación de secuencias. Debes crear un sistema que verifique automáticamente la calidad de secuencias de ADN.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision1_quality.sh`
2. Tu script debe:
   - Leer secuencias de ADN desde un array: `("ATCGATCG" "GCXTAGCTA" "AAAATTTT" "CCCCGGGG" "12345")`
   - Usar un bucle `while` para procesar cada secuencia
   - Usar `if-then-else` para validar que solo contenga A, T, C, G
   - Contar secuencias válidas e inválidas
   - Mostrar un reporte final

##### 📝 **Código de ejemplo para empezar:**
```bash
#!/bin/bash
# MISIÓN IMPOSIBLE - OPERACIÓN SEQUENCE QUALITY CONTROL
# Agente: [TU NOMBRE]
# Fecha: [FECHA ACTUAL]

echo "🧬 ACCESO CONCEDIDO - INICIANDO CONTROL DE CALIDAD"
echo "=================================================="

secuencias=("ATCGATCG" "GCXTAGCTA" "AAAATTTT" "CCCCGGGG" "12345")
# Tu código aquí...
```

---

#### 🔬 **MISIÓN 2: OPERACIÓN "AUTOMATED FILE SCANNER"**
**📍 Localización:** Centro de Gestión de Archivos

El villano ha eliminado archivos importantes. Debes crear un scanner automático que verifique la existencia y propiedades de archivos bioinformáticos.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision2_scanner.sh`
2. Tu script debe:
   - Crear una lista de archivos que debería existir: `("data.fasta" "results.txt" "config.bed" "output.vcf")`
   - Usar un bucle para verificar cada archivo
   - Para cada archivo, verificar si existe, si es legible, y su tamaño
   - Crear automáticamente los archivos faltantes (con `touch`)
   - Generar un reporte de seguridad

##### 🎪 **Diálogo dramático requerido:**
```bash
echo "🔍 INICIANDO ESCANEO DE SEGURIDAD..."
echo "📁 Verificando integridad del archivo: $archivo"
echo "⚠️  ALERTA: Archivo $archivo no encontrado!"
echo "✅ MISIÓN COMPLETADA - SISTEMA ASEGURADO"
```

---

#### 🧪 **MISIÓN 3: OPERACIÓN "GENE EXPRESSION ANALYZER"**
**📍 Localización:** Departamento de Análisis de Expresión

Dr. Chaos ha mezclado los datos de expresión génica. Debes crear un analizador que clasifique automáticamente los niveles de expresión.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision3_expression.sh`
2. Usar estos datos comprometidos:
   ```bash
   genes=("BRCA1" "TP53" "EGFR" "MYC" "PTEN")
   expression_levels=(2.5 0.3 15.8 0.1 8.2)
   ```
3. Tu script debe usar bucles y condicionales para:
   - Clasificar genes como: "Sobreexpresado" (>10), "Normal" (1-10), "Subexpresado" (<1)
   - Contar cuántos genes hay en cada categoría
   - Identificar el gen con mayor y menor expresión
   - Crear un reporte de análisis

##### 🎭 **Elemento dramático:**
```bash
echo "🔬 DESCIFRANDO PATRONES DE EXPRESIÓN GÉNICA..."
echo "📊 Procesando gen $gene con nivel $level"
echo "🧬 ANÁLISIS GENÓMICO COMPLETADO CON ÉXITO"
```

---

#### 💊 **MISIÓN 4: OPERACIÓN "DRUG RESISTANCE DETECTOR"**
**📍 Localización:** Laboratorio de Farmacogenómica

Para agentes elite. Crea un sistema que detecte automáticamente patrones de resistencia a medicamentos basado en mutaciones.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision4_resistance.sh`
2. Tu script debe:
   - Procesar secuencias con posibles mutaciones
   - Comparar con secuencias de referencia
   - Detectar mutaciones específicas asociadas con resistencia
   - Usar bucles `while` para leer un archivo de mutaciones
   - Generar alertas automáticas para mutaciones críticas

---

#### 🚀 **MISIÓN 5 (ULTRA SECRETA): OPERACIÓN "GENOMIC PIPELINE AUTOMATION"**
**📍 Localización:** Centro de Comando Genómico

Solo para agentes con máxima experiencia. Crea un pipeline completo que combine todas las habilidades aprendidas.

##### 🎯 **Objetivos:**
1. Crear un script maestro llamado `mision5_pipeline.sh`
2. Tu script debe:
   - Ejecutar automáticamente las 4 misiones anteriores
   - Verificar que cada misión se complete exitosamente
   - Generar un reporte consolidado
   - Usar estructuras `while` para monitoreo continuo
   - Implementar un sistema de logs de seguridad

---

### 📋 INFORME DE MISIÓN (ENTREGABLE)

#### 📝 **Debes entregar:**

1. **📁 Carpeta con tus scripts:**
   - `mision1_quality.sh`
   - `mision2_scanner.sh`
   - `mision3_expression.sh`
   - `mision4_resistance.sh` (opcional)
   - `mision5_pipeline.sh` (ultra secreta)

2. **📸 Capturas de pantalla mostrando:**
   - La ejecución de cada script
   - Los resultados obtenidos
   - El comando `ls -la` mostrando los permisos de ejecución

3. **📄 Reporte de agente (`informe_mision_while_if.txt`):**
   ```
   ================================
   INFORME DE MISIÓN CLASIFICADO
   ================================
   Agente: [TU NOMBRE]
   Fecha: [FECHA]
   Operación: WHILE-IF-007

   MISIÓN 1 - STATUS: [COMPLETADA/FALLIDA]
   Bucles while utilizados: [Describe cómo usaste while]
   Estructuras if implementadas: [Qué condicionales creaste]
   Secuencias válidas encontradas: [Número]
   
   MISIÓN 2 - STATUS: [COMPLETADA/FALLIDA]
   Archivos verificados: [Lista de archivos]
   Archivos creados automáticamente: [Cuáles faltaban]
   
   MISIÓN 3 - STATUS: [COMPLETADA/FALLIDA]
   Genes sobreexpresados: [Número y cuáles]
   Genes subexpresados: [Número y cuáles]
   Gen con mayor expresión: [Cuál y valor]

   MISIÓN 4 - STATUS: [COMPLETADA/FALLIDA/NO INTENTADA]
   Mutaciones detectadas: [Número]
   Resistencias identificadas: [Cuáles]

   MISIÓN 5 - STATUS: [COMPLETADA/FALLIDA/NO INTENTADA]
   Pipeline ejecutado: [SÍ/NO]
   Reportes generados: [Número]

   TÉCNICAS APRENDIDAS:
   - [¿Qué aprendiste sobre bucles while?]
   - [¿Cómo te ayudaron las estructuras if-then-else?]
   - [¿Qué operadores de comparación fueron más útiles?]

   DESAFÍOS ENFRENTADOS:
   - [¿Qué dificultades tuviste con while vs for?]
   - [¿Cómo resolviste problemas con las condiciones?]

   REFLEXIÓN FINAL:
   - [¿Cómo combinarías while e if en proyectos reales?]
   - [¿Qué análisis bioinformáticos automatizarías?]
   
   FIN DEL INFORME
   ================================
   ```

### 🏆 CRITERIOS DE EVALUACIÓN

- **Funcionalidad:** ¿Los scripts funcionan correctamente con while e if?
- **Lógica de control:** ¿Usaste estructuras condicionales apropiadamente?
- **Bucles while:** ¿Implementaste bucles while de manera efectiva?
- **Operadores:** ¿Aplicaste operadores de comparación correctos?
- **Documentación:** ¿Comentaste bien tu código y lógica?

---

## 📚 Recursos Adicionales

### Comandos útiles

```bash
# basename: extraer nombre de archivo
basename /usr/bin/sort

# dirname: extraer directorio
dirname /usr/bin/sort

# Variables de longitud
cadena="ATCGATCG"
echo ${#cadena}  # Muestra 8
```

### Ejemplos de archivos de prueba

#### Crear archivo FASTA de prueba
```bash
cat > clock.fasta << EOF
>secuencia1
ATCGATCGATCG
>secuencia2
GCTAGCTAGCTA
>secuencia3
TTTTAAAACCCC
EOF
```

#### Crear archivo BED de prueba
```bash
cat > archivo.bed << EOF
chr1	1000	2000	gene1
chr2	3000	4000	gene2
chr3	5000	6000	gene3
EOF
```

---

## 💡 Consejos para el Éxito

1. **Practica bucles while paso a paso:** Empieza con condiciones simples
2. **Combina estructuras:** Usa if dentro de while para mayor control
3. **Prueba operadores:** Experimenta con -eq, -ne, -gt, -lt
4. **Debug con echo:** Imprime valores para verificar condiciones
5. **Maneja casos extremos:** ¿Qué pasa si un archivo no existe?

### Errores comunes a evitar

```bash
# ❌ Incorrecto - espacios faltantes
if [$var -eq 5]; then

# ✅ Correcto - espacios necesarios
if [ $var -eq 5 ]; then

# ❌ Incorrecto - bucle infinito sin incremento
while [ $i -lt 10 ]
do
    echo $i
    # Falta: i=$((i+1))
done

# ✅ Correcto - incremento incluido
while [ $i -lt 10 ]
do
    echo $i
    i=$((i+1))
done
```

**¡El control de flujo es la clave para automatizar la bioinformática! 🚀🧬**

---

## 📖 Referencias

- Blum, R., & Bresnahan, C. (2021). Linux command line and Shell scripting bible (Fourth edition). Wiley. Capítulo 11.

---

### 🎯 Próximos Pasos

Después de completar esta sesión, estarás preparado para:
- Crear pipelines de análisis automatizados
- Procesar grandes volúmenes de datos biológicos
- Implementar control de calidad en tus scripts
- Combinar múltiples herramientas de bioinformática

¿Te sientes preparado para ser un experto en control de flujo? 🕵️‍♂️
