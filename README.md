![Wallpaper](https://raw.githubusercontent.com/JVR-07/College-Projects/refs/heads/main/Resource/wallpaper_itt.png)
# Analizador Léxico Multilenguaje – JavaCC
Este proyecto implementa un **analizador léxico** desarrollado con **JavaCC (Java Compiler Compiler)**, diseñado para reconocer y clasificar tokens de diferentes lenguajes de programación.
El analizador fue entrenado con más de **300 palabras clave**, que abarcan conceptos de **C, C++, Java, Python, JavaScript, Rust, SQL**, entre otros.

El objetivo es **identificar** los componentes léxicos (**tokens**) de un **texto fuente** y clasificarlos por tipo, facilitando la etapa de análisis sintáctico en futuros compiladores o intérpretes.
# Características principales
- Basado en JavaCC, con reglas definidas en el archivo `main.jj`.
- Clasifica más de 300 palabras reservadas y operadores.
- Modo interactivo o lectura desde archivo `.txt`.
- Implementa un mapeo automático de tokens mediante reflexión de `MainConstants`.

**Reconoce:**
- Palabras reservadas.
- Operadores aritméticos, lógicos, relacionales y bitwise.
- Estructuras de control.
- Tipos de datos y modificadores.
- Identificadores, cadenas y números.
- Comentarios y espacios en blanco.
# Estructura del proyecto
```graphql
Analizador-Lexico/
├── main.jj               # Archivo principal JavaCC: define tokens y gramática
├── Main.java             # Programa ejecutable generado y adaptado
├── MainConstants.java    # Constantes generadas automáticamente por JavaCC
├── MainTokenManager.java # Manejador de tokens
├── palabras.txt          # Archivo .txt que contiene todas las palabras
└── codigo-simulado.txt   # Archivo .txt que simula texto fuente de programación
```
# Ejecución
## 1. Generar el analizador con JavaCC
```bash
javacc main.jj
```
Esto genera los archivos necesarios: `Main.java`, `MainTokenManager.java`, `Token.java`, `MainConstants.java`, etc.
## 2. Compilar el proyecto
```bash
javac *.java
```
## 3. Ejecutar el analizador
```bash
java Main
```
# Modos de uso
## Modo interactivo
Permite escribir fragmentos de código directamente desde la terminal:
```java
=== Analizador Léxico ===
1. Ingresar texto manualmente
2. Analizar archivo .txt
3. Salir
> 1
Modo interactivo (Ctrl + C o 'salir' para terminar)
> if (x > 5) print("Hola");
→ Token: if              | Tipo: <PREGUNTAR>
→ Token: (               | Tipo: <PAREN_IZQ>
→ Token: x               | Tipo: <VARIABLE>
→ Token: >               | Tipo: <COMPARACION>
→ Token: 5               | Tipo: <ENTERO>
→ Token: )               | Tipo: <PAREN_DER>
→ Token: print           | Tipo: <IMPRIMIR>
→ Token: (               | Tipo: <PAREN_IZQ>
→ Token: "Hola"          | Tipo: <CADENA_DOBLE>
→ Token: )               | Tipo: <PAREN_DER>
→ Token: ;               | Tipo: <PUNTOCOMA>
```
## Modo por texto fuente
```java
> 2
Nombre del archivo .txt: ejemplo.txt
→ Token: while           | Tipo: <CICLO>
→ Token: i               | Tipo: <VARIABLE>
→ Token: <               | Tipo: <COMPARACION>
→ Token: 10              | Tipo: <ENTERO>
...
```
# Funcionamiento interno
## 1. Definición de tokens
En `main.jj` se definen las **expresiones regulares** que identifican cada **token**. Ejemplo:
```java
TOKEN : {
  < PREGUNTAR: "if" > |
  < SINO: "else" > |
  < CICLO: "while" | "loop" >
}
```
## 2. Generación del analizador
**JavaCC** convierte estas reglas en una clase **`MainTokenManager`** que genera los tokens al leer una secuencia de caracteres.
## 3. Ejecución del programa
`Main.java` utiliza `MainTokenManager` y `SimpleCharStream` para leer texto y mostrar cada token identificado con su tipo.
# Conclusiones
- **JavaCC** es una herramienta poderosa para construir **analizadores léxicos y sintácticos**.
- El proyecto demuestra cómo reconocer múltiples lenguajes en una sola gramática.
- La modularidad de `main.jj` facilita extender el analizador para futuras fases de compilación (parser, AST, etc.).
- La clasificación de 300 palabras clave abarca las estructuras fundamentales de varios lenguajes modernos, lo que lo hace una excelente base para un analizador léxico multilenguaje.
# Autor
**Javier Machado Sánchez.**
Instituto Tecnológico de Tijuana.
**Materia**: Lenguajes y Autómatas II.
Profesor: Erasmo Estrada Peña.
30 de Octubre del 2025.
# Lista de tokens
## Palabras Reservadas
| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| PREGUNTAR | `"if"` | if |
| SINO | `"else"` | else |
| HACER | `"do"` | do |
| CICLO | `"while" \| "loop"` | while, loop |
| CICLO_HASTA | `"for"` | for |
| FUNCION | `"function" \| "def" \| "fn" \| "lambda"` | function, def, fn, lambda |
| REGRESAR | `"return" \| "yield"` | return, yield |
| CLASE | `"class"` | class |
| HERENCIA | `"extends"` | extends |
| INTERFAZ | `"interface" \| "trait"` | interface, trait |
| IMPLEMENTA | `"implements" \| "impl"` | implements, impl |
| ESTRUCTURA | `"struct"` | struct |
| IMPORTAR | `"import" \| "require" \| "crate"` | import, require, crate |
| EXPORTAR | `"export"` | export |
| USAR | `"using" \| "use"` | using, use |
| ORIGEN | `"from"` | from |
| MODULO | `"mod"` | mod |
| TAMAÑO_DE | `"sizeof"` | sizeof |
| ALINEAMIENTO_DE | `"alignof"` | alignof |
| INSEGURO | `"unsafe"` | unsafe |
| IMPRIMIR | `"print" \| "println" \| "write"` | print, println, write |
## Operadores
| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| ARITMETICA | `"+" \| "-" \| "*" \| "/" \| "%"` | +, -, *, /, % |
| UNARIOS | `"**" \| "++" \| "--"` | **, ++, -- |
| ASIGNACION | `"=" \| "+=" \| "-=" \| "*=" \| "/=" \| "%=" \| ":"` | =, +=, -=, *=, /=, %=, : |
| COMPARACION | `"==" \| "===" \| "equals" \| "!=" \| "!==" \| "<" \| ">" \| "<=" \| ">="` | \==, =\==, equals, !=, !==, <, >, <=, >= |
| LOGICOS | `"&&" \| "\|\|" \| "!" \| "and" \| "or" \| "not"` | &&, \|\|, !, and, or, not |
| BITWISE | `"&" \| "\|" \| "^" \| "~" \| "<<" \| ">>" \| ">>>"` | &, \|, ^, ~, <<, >>, >>> |
| ASIGNACION_COMPUESTA | `"&=" \| "\|=" \| "^=" \| "<<=" \| ">>=" \| ">>>="` | &=, \|=, ^=, <<=, >>=, >>>= |
| OPERADOR_TRES_VIAS | `"<=>"` | <=> |
| OPERADOR_COALESCENCIA | `"??"` | ?? |
| OPERADOR_SEGURO | `"?"` | ? |
| OPERADOR_TERNARIO | `"?:“` | ?: |
| OPERADOR_ENCADENADOR | `"\|>"` | \|> |
| FLECHA | `"=>" \| "->"` | =>, -> |
| RESOLUCION_AMBITO | `"::"` | :: |
| SPREAD | `"..."` | ... |
| RANGO | `".." \| "..="` | .., ..= |
## Tipos y Variables
| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| DATO_DINAMICO | `"var" \| "let" \| "dynamic" \| "dyn"` | var, let, dynamic, dyn |
| DATO_CADENA | `"string"` | string |
| DATO_CARACTER | `"char"` | char |
| DATO_BYTE | `"byte"` | byte |
| DATO_DECIMAL | `"float" \| "double" \| "decimal"` | float, double, decimal |
| DATO_ESTATICO | `"int" \| "long" \| "short" \| "bigint"` | int, long, short, bigint |
| DATO_COMPLEJO | `"complex"` | complex |
| DATO_BINARIO | `"boolean"` | boolean |
| CONSTANTE | `"const"` | const |
| MODIFICADOR | `"abstract" \| "static" \| "final" \| "readonly" \| "constexpr" \| "mutable" \| "volatile" \| "mut"` | abstract, static, final, readonly, constexpr, mutable, volatile, mut |
| DATO_VACIO | `"null" \| "undefined" \| "None"` | null, undefined, None |
| PROCEDIMIENTO | `"void"` | void |
| BANDERA | `"true" \| "false"` | true, false |
| NUEVO | `"new"` | new |
| ACCESO | `"public" \| "private" \| "protected" \| "pub"` | public, private, protected, pub |
| PAQUETE | `"package" \| "namespace" \| "global"` | package, namespace, global |
| TIPO_INSTANCIA | `"instanceof"` | instanceof |
| TIPO_DATO | `"typeof"` | typeof |
| TIPO_FUNCION | `"typedef"` | typedef |
| TIPO_PROPIO | `"self" \| "Self"` | self, Self |
| VECTOR | `"vector"` | vector |
| DATO_ENTERO_SIN_SIGNO | `"uint" \| "ulong" \| "ushort" \| "sbyte"` | uint, ulong, ushort, sbyte |
| DATO_COLECCION | `"array" \| "list" \| "dict" \| "arr"` | array, list, dict, arr |

## Control y Excepciones

| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| INTENTA | `"try"` | try |
| ATRAPA | `"catch"` | catch |
| FINAL | `"finally"` | finally |
| LANZA | `"throw" \| "throws"` | throw, throws |
| PANICO | `"panic!"` | panic! |
| ELIGE | `"switch"` | switch |
| CASO | `"case"` | case |
| POR_DEFECTO | `"default"` | default |
| COINCIDE | `"match"` | match |
| CONTINUAR | `"continue"` | continue |
| DETENER | `"break"` | break |
| VE_A | `"goto"` | goto |
| EN | `"in" \| "on"` | in, on |

## Concurrencia, Asincronía y Referencias

| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| SINCRONIZADO | `"synchronized"` | synchronized |
| ASINCRONICO | `"async" \| "tokio"` | async, tokio |
| ESPERA | `"await"` | await |
| EXPLICITO | `"explicit"` | explicit |
| OPERADOR | `"operator"` | operator |
| COMO | `"as"` | as |
| ES | `"is"` | is |
| CONVERSION_DINAMICA | `"dynamic_cast"` | dynamic_cast |
| CONVERSION_ESTATICA | `"static_cast"` | static_cast |
| PLANTILLA | `"template"` | template |
| TIPO_PLANTILLA | `"typename"` | typename |
| REQUERIMIENTOS | `"requires"` | requires |
| CONCEPTO | `"concept"` | concept |
| TIPO_VARIABLE | `"typevar"` | typevar |
| REFERENCIA | `"ref"` | ref |
| SALIDA | `"out"` | out |
| MOVER | `"move" \| "mov"` | move, mov |
| PRESTAMO | `"borrow"` | borrow |
| TIEMPO_VIDA | `"lifetime"` | lifetime |
| ASIGNAR_MONTICULO | `"box"` | box |
| FIJAR_MEMORIA | `"fixed"` | fixed |
| ASIGNAR_STACK | `"stackalloc"` | stackalloc |
| HILO_LOCAL | `"thread_local"` | thread_local |
| DUERME | `"sleep"` | sleep |
| TIEMPO_ESPERA | `"timeout"` | timeout |
| APARECER | `"spawn"` | spawn |
| EVENTO | `"event"` | event |
| AGREGAR_EVENTO | `"add"` | add |
| REMOVER_EVENTO | `"remove"` | remove |
| DELEGADO | `"delegate"` | delegate |
| VALOR | `"value"` | value |
| OBTENER | `"get"` | get |
| ESTABLECER | `"set"` | set |
| COVARIANZA | `"covariant"` | covariant |
| CONTRAVARIANZA | `"contravariant"` | contravariant |

## SQL y LINQ

| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| SELECCIONAR | `"select"` | select |
| DONDE | `"where"` | where |
| AGRUPAR_POR | `"group by"` | group by |
| ORDENAR_POR | `"order by"` | order by |
| ASCENDENTE | `"ascending"` | ascending |
| DESCENDENTE | `"descending"` | descending |
| INSERTAR | `"insert"` | insert |
| ACTUALIZAR | `"update"` | update |
| ELIMINAR | `"delete"` | delete |
| TENIENDO | `"having"` | having |
| UNION | `"join"` | join |
| INTERNA | `"inner"` | inner |
| EXTERNA | `"outer"` | outer |
| IZQUIERDA | `"left"` | left |
| DERECHA | `"right"` | right |
| CRUZADA | `"cross"` | cross |
| NATURAL | `"natural"` | natural |
| UNION_RESULTADOS | `"union"` | union |
| INTERSECCION | `"intersect"` | intersect |
| EXCEPTO | `"except"` | except |
| DISTINTO | `"distinct"` | distinct |
| TODOS | `"all"` | all |
| CUALQUIER | `"any"` | any |
| ALGUN | `"some"` | some |
| EXISTE | `"exists"` | exists |
| ENTRE | `"between"` | between |
| COMO_SQL | `"like"` | like |
| PRIMARIO | `"primary"` | primary |
| FORANEO | `"foreign"` | foreign |
| REFERENCIAS | `"references"` | references |
| RESTRICCION | `"constraint"` | constraint |
| BD | `"database"` | database |
| TABLA | `"table"` | table |
| COLUMNA | `"column"` | column |
| FILA | `"row"` | row |
| ESQUEMA | `"schema"` | schema |
| VISTA | `"view"` | view |
| INDICE | `"index"` | index |
| DISPARADOR | `"trigger"` | trigger |
| TRANSACCIONES | `"transaction"` | transaction |
| MENSAJE | `"commit"` | commit |
| REVERTIR | `"rollback"` | rollback |
| CONCEDER | `"grant"` | grant |
| REVOCAR | `"revoke"` | revoke |
| ALTERAR | `"alter"` | alter |
| BORRAR | `"drop"` | drop |

## Rust y Macros

| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| MACRO | `"macro"` | macro |
| IMPRIMIR_MACRO | `"println!"` | println! |
| VECTOR_MACRO | `"vec!"` | vec! |
| ASERCION_MACRO | `"assert!"` | assert! |
| SELECCIONAR_MACRO | `"select!"` | select! |
| OPCIONAL | `"Option"` | Option |
| PRESENTE | `"Some"` | Some |
| RESULTADO | `"Result"` | Result |
| EXITOSO | `"Ok"` | Ok |
| ERROR | `"Err"` | Err |
| ITERADOR | `"Iterator"` | Iterator |
| CLONAR | `"Clone"` | Clone |
| COPIAR | `"Copy"` | Copy |
| HASH | `"Hash"` | Hash |
| CONTADOR_REFERENCIAS | `"Rc"` | Rc |
| EXCLUSION_MUTUA | `"Mutex"` | Mutex |
| CANAL | `"Channel"` | Channel |
| REMITENTE | `"Sender"` | Sender |
| RECEPTOR | `"Receiver"` | Receiver |
| SERIALIZACION | `"serde"` | serde |
## Símbolos Síntacticos
| Token | Expresión Regular | Lexema |
| ------ | ---------------- | ------- |
| PAREN_IZQ | `"("` | ( |
| PAREN_DER | `")"` | ) |
| LLAVE_IZQ | `"{"` | { |
| LLAVE_DER | `"}"` | } |
| CORCHETE_IZQ | `"["` | [ |
| CORCHETE_DER | `"]"` | ] |
| PUNTOCOMA | `";"` | ; |
| COMA | `","` | , |

## Identificadores y Variables

| Token | Expresión Regular | Ejemplo |
| ------ | ---------------- | -------- |
| VARIABLE | `(<LETRA> \| <GUION_BAJO>)(<LETRA> \| <DIGITO> \| <GUION_BAJO>)*` | _nombreVariable3 |
| ENTERO | `<DIGITO>(<DIGITO>)*` | 123 |
| DECIMAL | `(<DIGITO>)*"."(<DIGITO>)*` | 12.34 |
| CADENA_DOBLE | `"\"(<LETRA> \| <DIGITO> \| <GUION_BAJO> \| <PUNTO>)*\""` | "hola" |
| CADENA_SIMPLE | `"\'(<LETRA> \| <DIGITO> \| <GUION_BAJO> \| <PUNTO>)*\'"` | 'hola' |
| COMENTARIO_LINEA | `"//"(<CUERPO_COMENTARIO>)*` | // comentario |
| ESPACIO | `<ESPACIO_BLANCO>(<ESPACIO_BLANCO> \| <TABULADOR> \| <RETORNO_CARRO> \| <NUEVA_LINEA>)*` | espacio, tab, salto |
