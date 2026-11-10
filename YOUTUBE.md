# Cómo buscar en YouTube para practicar PHP (solo lo del examen)

> Objetivo: encontrar vídeos **cortos y concretos** de lo que entra, sin perder tiempo con cosas que **no hemos dado**.

---

## 1. Reglas para buscar bien

1. **Busca un tema concreto, no "curso de PHP".** Un curso completo de 10 h te va a meter cosas que no entran.
2. **Añade siempre `php`** y, si quieres en español, **`español`** o **`desde cero`**.
3. **Mejor vídeos de 5–20 min.** En YouTube: *Filtros → Duración → 4-20 minutos*.
4. **Mejor recientes** (PHP 7 / PHP 8). *Filtros → Fecha de subida → Este año* si salen cosas muy antiguas.
5. **Mira la miniatura y el título**: si pone **Laravel, MySQL, POO/clases, sesiones, arrays, funciones propias, AJAX, JavaScript** → **sáltalo** (no entra).
6. Usa **velocidad 1.25x–1.5x** y **pausa para escribir tú el código** en XAMPP. Ver sin escribir no sirve.
7. En inglés hay más y mejores vídeos: añade la palabra en inglés entre paréntesis de la tabla.

---

## 2. Qué buscar, tema por tema

Copia y pega la búsqueda tal cual. Están en el orden de los ejercicios.

### Ejercicio 1 – Variables, echo/print, concatenación, heredoc

| Tema | Búsqueda en español | Búsqueda en inglés |
|---|---|---|
| Primer programa | `php desde cero xampp primer programa` | `php tutorial for beginners xampp` |
| Variables | `php variables tutorial español` | `php variables beginners` |
| echo vs print | `php diferencia echo y print` | `php echo vs print` |
| Comillas | `php comillas simples y dobles diferencia` | `php single vs double quotes` |
| Concatenar | `php concatenar cadenas punto` | `php string concatenation` |
| Heredoc | `php heredoc cadena multilinea` | `php heredoc syntax` |
| Operadores | `php operadores aritmeticos modulo` | `php arithmetic operators modulus` |

### Ejercicio 2 – Formularios GET y POST

| Tema | Búsqueda en español | Búsqueda en inglés |
|---|---|---|
| Formulario básico | `php formulario html recibir datos` | `php form handling tutorial` |
| GET vs POST | `php get y post diferencia formulario` | `php get vs post` |
| filter_input | `php filter_input INPUT_POST` | `php filter_input tutorial` |
| Select y textarea | `formulario html select optgroup textarea` | `html form select optgroup textarea` |
| Calculadora | `calculadora php formulario` | `php simple calculator form` |

### Ejercicio 3 – if / elseif / else y validaciones

| Tema | Búsqueda en español | Búsqueda en inglés |
|---|---|---|
| Condicionales | `php if else elseif tutorial` | `php if else elseif` |
| Operadores lógicos | `php operadores logicos and or` | `php logical operators` |
| Mayor de 3 números | `php mayor de tres numeros` | `php largest of three numbers` |
| Validar campos vacíos | `php validar formulario campos vacios isset` | `php form validation empty fields isset` |
| trim | `php funcion trim` | `php trim function` |
| Saludo según hora | `php getdate hora saludo buenos dias` | `php getdate function` |
| str_pad | `php str_pad ceros a la izquierda` | `php str_pad leading zeros` |

### Ejercicio 4 – switch

| Tema | Búsqueda en español | Búsqueda en inglés |
|---|---|---|
| switch | `php switch case break tutorial` | `php switch statement` |
| Letra del DNI | `calcular letra dni php` | — (es algo español) |
| Nota media | `php calcular nota media formulario` | `php average grade calculator` |
| Redondeos | `php round floor ceil diferencia` | `php round floor ceil` |

### Ejercicio 5 – Bucles

| Tema | Búsqueda en español | Búsqueda en inglés |
|---|---|---|
| for | `php bucle for tutorial` | `php for loop` |
| while / do while | `php while y do while diferencia` | `php while vs do while` |
| Generar select con bucle | `php llenar select con for` | `php generate dropdown options loop` |
| Tabla multiplicar | `tabla de multiplicar php for formulario` | `php multiplication table form` |
| Pirámide asteriscos | `piramide asteriscos php for` | `php star pattern for loop` |
| Número primo | `numero primo php` | `php check prime number` |
| Divisores | `divisores de un numero php` | `php find divisors of a number` |
| Fibonacci | `serie fibonacci php for` | `php fibonacci series loop` |
| Pares / impares | `numeros pares php for` | `php even numbers loop` |

---

## 3. Canales que suelen tener PHP para principiantes

No hace falta seguir un curso entero: entra al canal, busca dentro de él (lupa 🔍 en la página del canal) el tema que te toque.

**Español**
- **Píldoras Informáticas** – curso de PHP muy pausado y por temas (vídeos cortos).
- **Fazt** – vídeos prácticos, a veces van rápido.
- **codigofacilito** / **Bluuweb** / **HolaMundo** – busca dentro "php".

**Inglés**
- **Bro Code** – "PHP Full Course": va por temas con marcas de tiempo (capítulos). Salta directo a *variables, if, switch, for, while, forms (GET/POST)*.
- **Programming with Mosh** / **Traversy Media** – introducciones a PHP.

> ⚠️ En los cursos largos usa los **capítulos** (las marcas de tiempo bajo el vídeo) y **para cuando empiecen arrays, funciones propias, sesiones o bases de datos**: ya no entra.

---

## 4. Cómo practicar con un vídeo (método de 20 min)

1. **Mira** el vídeo una vez sin escribir (velocidad 1.5x).
2. **Cierra el vídeo** y escribe tú el código en `htdocs` → ábrelo en `http://localhost/...`.
3. Si te atascas, vuelve **solo al trozo** que necesitas.
4. **Cámbialo**: hazlo con GET en vez de POST, con `while` en vez de `for`, añade una validación con mensaje en rojo (`class='fallo'`)...
5. Pasa a la web de repaso (`repaso.html`) y haz los ejercicios de ese tema.

---

## 5. Búsquedas "tipo examen" (mezclan varios temas)

Estas son las más parecidas a lo que te pueden poner:

```
php formulario validar campos vacios mensaje error
php formulario select calcular resultado switch
php formulario mismo archivo isset submit
php tabla de multiplicar formulario mismo archivo
php ejercicios resueltos principiantes formularios
php ejercicios resueltos bucles for while
php ejercicios resueltos condicionales if switch
```

> Si buscas **"ejercicios resueltos"** te saldrán listas de ejercicios: intenta hacerlos **antes** de ver la solución.
