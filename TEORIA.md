# TEORÍA PHP – IAW · UD2 (Ejercicios 1 a 5)

> Resumen de **solo lo que hemos dado** en los ejercicios 1A → 5B.
> Cada apartado dice en qué ejercicio salió, para que puedas ir al código.

---

## Índice

0. [Cómo se estructuran los ejercicios](#0-cómo-se-estructuran-los-ejercicios)
1. [Lo básico: etiquetas PHP, `;` y comentarios](#1-lo-básico)
2. [Variables y tipos](#2-variables)
3. [Mostrar datos: `echo` y `print`](#3-mostrar-datos-echo-y-print)
4. [Comillas dobles, simples y escapar caracteres](#4-comillas-dobles-vs-simples)
5. [Concatenación: `.` y `.=`](#5-concatenación)
6. [Cadenas multilínea (heredoc)](#6-cadenas-multilínea-heredoc)
7. [Operadores aritméticos y de asignación](#7-operadores-aritméticos)
8. [Funciones de redondeo y raíz cuadrada](#8-redondeos-y-raíz)
9. [Formularios HTML](#9-formularios-html)
10. [Recoger datos en PHP: `filter_input`](#10-recoger-datos-filter_input)
11. [Estructuras alternativas: `if / elseif / else`](#11-if--elseif--else)
12. [Validar datos (vacíos, repetidos, faltantes)](#12-validaciones)
13. [Estructura `switch`](#13-switch)
14. [Fecha y hora: `getdate`, `str_pad`, meta refresh](#14-fecha-y-hora)
15. [Bucles: `for`, `while`, `do…while`](#15-bucles)
16. [Patrones típicos con bucles](#16-patrones-típicos-con-bucles)
17. [Formulario que se envía a sí mismo](#17-formulario-que-se-envía-a-sí-mismo)
18. [Errores típicos (¡sacados de los ejercicios!)](#18-errores-típicos)
19. [Chuleta de 1 página](#19-chuleta-final)

---

## 0. Cómo se estructuran los ejercicios

Casi todos los ejercicios tienen **2 ficheros + 1 CSS**:

```
EjercicioXX.html   → el FORMULARIO (lo que ve el usuario)
ejercicioXX.php    → el PROCESO (recoge datos, calcula y muestra el resultado)
EjercicioXX.css    → estilos (clases que usamos: .centrar y .fallo → texto rojo)
```

Flujo:

```
[Formulario .html]  --(submit)-->  [proceso .php]  --(HTML generado)-->  navegador
     action="ejercicioXX.php"         filter_input(...)
     method="get" o "post"            if / switch / bucles
                                      print / echo
                                      <a href="EjercicioXX.html">Volver</a>
```

A partir del **5A** el formulario pasa a ser **`.php`**, porque las opciones de las listas se generan con bucles.
En el **5B** algunos ejercicios son **un solo `.php`** que contiene el formulario y el resultado (se envía a sí mismo).

Esqueleto típico de un `.php` de resultado (estilo del profe):

```php
<!DOCTYPE html>
<html>
  <head>
    <title>Resultado</title>
    <meta charset="utf-8" />
    <link rel="stylesheet" type="text/css" href="Ejercicio3B.css" />
  </head>
  <body>
    <h1>Resultado...</h1>
    <fieldset>
    <?php
      // 1. Recoger datos
      $n1 = filter_input(INPUT_GET, "cant1");
      // 2. Validar
      // 3. Calcular
      // 4. Visualizar
      print "<h3>...</h3>";
    ?>
    <p class='centrar'><a href="Ejercicio3B.html">Volver</a></p>
    </fieldset>
  </body>
</html>
```

> 💡 En el examen sigue este orden: **recoger → validar → procesar → visualizar**. Es justo lo que comenta el profe en su código.

---

## 1. Lo básico

```php
<?php
    // código PHP
?>
```

- PHP se ejecuta en el **servidor** (XAMPP/Apache). El navegador solo recibe el **HTML resultante**.
  Por eso los `.php` hay que abrirlos con `http://localhost/...`, no con doble clic.
- Cada instrucción termina en **`;`**.
- Se puede **mezclar HTML y PHP** en el mismo fichero, abriendo y cerrando `<?php ?>` las veces que haga falta (lo hiciste así en el 1A):

```php
<p>Contenido de la variable $var1: <?php print($var1); ?></p>
```

### Comentarios

```php
// comentario de una línea
#  comentario de una línea (también vale)
/* comentario
   de varias líneas */
```

---

## 2. Variables

- Empiezan **siempre por `$`**: `$var1`, `$nombre`, `$nombre_completo`.
- **No se declara el tipo**: PHP lo deduce por el valor.
- Distinguen **mayúsculas/minúsculas**: `$Nombre` ≠ `$nombre`.
- No pueden empezar por número ni tener espacios ni guiones (`$nombre-completo` ❌ → `$nombre_completo` ✅).

```php
$var1 = 5;            // entero (int)
$var2 = 2;            // entero
$division = 2.5;      // decimal (float)
$nombre = "Pepe";     // texto (string)
$apellido = 'Ruiz';   // texto
$primo = true;        // booleano (true / false)  → usado en 5B ejercicio 5
```

---

## 3. Mostrar datos: `echo` y `print`

Los dos sacan texto/HTML a la página.

```php
print "Hola";
print("Hola");          // con paréntesis también vale
echo "Hola";
echo 'Suma: ', $suma, "<br />";   // echo admite VARIOS valores separados por comas
```

| | `echo` | `print` |
|---|---|---|
| Varios valores con `,` | ✅ | ❌ (solo uno) |
| Paréntesis opcionales | ✅ | ✅ |
| Resultado en pantalla | igual | igual |

Lo que imprimes puede ser **HTML**:

```php
print "<h3>Resultados</h3>";
print "<p>Valor: <b>$var1</b></p>";
```

---

## 4. Comillas dobles vs simples

| Comillas | ¿Sustituye variables? | Ejemplo | Sale |
|---|---|---|---|
| **Dobles** `" "` | ✅ Sí | `"Hola $nombre"` | `Hola Pepe` |
| **Simples** `' '` | ❌ No | `'Hola $nombre'` | `Hola $nombre` |

### Escapar caracteres con `\` (dentro de comillas dobles / heredoc)

```php
print "Contenido de la variable \$var1: $var1";   // → Contenido de la variable $var1: 5
print "Dijo \"hola\"";                              // → Dijo "hola"
```

- `\$` → muestra el símbolo `$` literalmente (lo usa el profe en el 1A/1B/1C).
- `\"` → comilla doble dentro de comillas dobles.

Truco muy usado: **comillas simples dentro de dobles** para los atributos HTML:

```php
print "<h3 class='fallo'>Valores repetidos</h3>";
print "<option value='$i'>$i</option>";
```

O al revés, escapando: `echo "<option value=\"$i\">$i</option>";` (lo hiciste así en 5A).

### Entidades HTML que salen en los ejercicios

| Escribes | Se ve |
|---|---|
| `&lt;` | `<` |
| `&gt;` | `>` |
| `&nbsp;` | espacio |
| `&#176;` | ° |

Ej: `<a href='Ejercicio3B.html'>&lt;&lt;&lt; Volver</a>` → `<<< Volver` · `$media -&gt; Notable` → `7 -> Notable`.

---

## 5. Concatenación

El operador para **unir textos** es el **punto `.`** (¡no el `+`!).

```php
$nombre_completo = $nombre . " " . $apellido;   // "Pepe Ruiz"
$dire = $dire . '-' . $cp;                        // "Calle Mayor 3-48001"
print "<b>" . $var1 . "</b>";
```

### Operador `.=` (concatenar y asignar)

```php
$nombre .= ' ' . $ape1 . ' ' . $ape2;
// es lo mismo que:
$nombre = $nombre . ' ' . $ape1 . ' ' . $ape2;
```

Se usa mucho para **ir acumulando** texto (3C, 5B-4):

```php
$linea = "";
$linea = $linea . "*";   // o  $linea .= "*";
```

---

## 6. Cadenas multilínea (heredoc)

Sirve para escribir **mucho HTML con variables** sin poner `print` en cada línea (Ejercicio 1C, 2A, 2B, 4A).

```php
print <<<RDO
<h3>Valores de partida</h3>
<p>
  Contenido de la variable <i>\$var1</i>: <b>$var1</b><br />
  Contenido de la variable <i>\$var2</i>: <b>$var2</b>
</p>
RDO;
```

Reglas:
- Empieza con **`<<<IDENTIFICADOR`** (el nombre lo eliges tú: `RDO`, `END`, `EJEMPLO`, `RESULTADO`, `HTML`...).
- Termina con **el mismo identificador** seguido de **`;`**, solo en su línea.
- Se comporta como **comillas dobles**: sustituye `$variables` y hay que usar `\$` para ver un `$`.
- En PHP moderno (7.3+) el cierre puede ir **indentado** (como en tus ejercicios). El profe lo pone pegado a la izquierda (columna 0): así **funciona siempre**.

Se puede **guardar en una variable** y mostrarla después (lo hace el profe en 1C):

```php
$visualizar = <<<RDO
<h3>Resultados</h3>
<p>Suma: <b>$suma</b></p>
RDO;

print $visualizar;
```

---

## 7. Operadores aritméticos

| Operador | Significado | `$var1=5; $var2=2;` |
|---|---|---|
| `+` | suma | `7` |
| `-` | resta | `3` |
| `*` | producto | `10` |
| `/` | división (puede dar decimales) | `2.5` |
| `%` | **resto** (módulo) | `1` |

Prioridad: primero `*`, `/`, `%`, después `+`, `-`. Usa paréntesis para cambiarla:

```php
$media = ($aso + $asgbd + $eie + $iaw + $in + $sad + $sri) / 7;   // ¡paréntesis obligatorios!
```

### `%` (resto) es CLAVE en el examen

- Letra del DNI → `$dni % 23`
- Saber si es par → `$n % 2 == 0`
- Divisores / primos → `$numero % $i == 0` (división exacta)

### Operadores de asignación / incremento

```php
$i = $i + 1;   // forma larga
$i += 1;       // igual
$i++;          // igual (incrementa en 1)
$i--;          // decrementa en 1
$i += 2;       // suma 2 (pares)
$i -= 2;       // resta 2 (pares hacia atrás)
$texto .= "*"; // concatena y asigna
```

---

## 8. Redondeos y raíz

Vienen comentados en el 4B del profe:

| Función | Qué hace | `3.6` | `3.4` |
|---|---|---|---|
| `round($x)` | redondea al más cercano | `4` | `3` |
| `floor($x)` | redondea **hacia abajo** | `3` | `3` |
| `ceil($x)` | redondea **hacia arriba** | `4` | `4` |
| `(int)($x)` | **corta** los decimales | `3` | `3` |

```php
$media = round(($aso + $asgbd + $eie + $iaw + $in + $sad + $sri) / 7);   // profe
$media = (int) (($nota1 + ... + $nota7) / 7);                             // tú
```

⚠️ No dan lo mismo: con media 6.7 → `round` = **7 (Notable)**, `(int)` = **6 (Bien)**. El profe usó `round`.

**Raíz cuadrada**: `sqrt($numero)` → se usa en el ejercicio del número primo (5B-5).

---

## 9. Formularios HTML

```html
<form method="get" action="ejercicio2A.php">
  <fieldset>
    <legend>Datos</legend>
    <label>Teclea tu nombre:
      <input type="text" name="NombreUsuario" value="" />
    </label>
    <input type="submit" value="Enviar" />
    <input type="reset" value="Limpiar" />
  </fieldset>
</form>
```

### Atributos de `<form>`

| Atributo | Para qué |
|---|---|
| `action` | fichero PHP que **recibe y procesa** los datos |
| `method` | `get` o `post` |

### GET vs POST

| | GET | POST |
|---|---|---|
| Dónde viajan los datos | en la **URL** (`?nombre=Pepe&cp=48001`) | ocultos, en el cuerpo de la petición |
| Se ven / se pueden guardar en favoritos | sí | no |
| En PHP se recogen con | `INPUT_GET` | `INPUT_POST` |

El profe usa **GET**, tú usaste **POST**. Los dos valen, **pero el `method` del formulario y el `INPUT_...` del PHP tienen que coincidir**.

### Controles que hemos usado

```html
<!-- Cuadro de texto -->
<input type="text" name="nombre" />
<input type="text" name="cp" size="4" maxlength="5" />   <!-- size: ancho visible · maxlength: máx caracteres -->
<input type="text" name="dni" size="8" maxlength="8" />  <!-- 4A -->

<!-- Número -->
<input type="number" name="numero" />

<!-- Lista de selección -->
<select size="1" name="estudios">
  <option value="0"> --- Selecciona --- </option>
  <optgroup label="Informática y Comunicaciones">       <!-- agrupa opciones (2B) -->
    <option value="ASIR">Administración de Sistemas Informáticos en Red</option>
    <option value="DAW">Desarrollo de Aplicaciones Web</option>
  </optgroup>
</select>

<!-- Área de texto -->
<textarea name="comentarios" rows="10" cols="40" placeholder="Escribe aquí..."></textarea>

<!-- Botones -->
<input type="submit" value="Enviar Datos" />      <!-- envía -->
<input type="reset"  value="Limpiar" />           <!-- borra lo escrito/seleccionado -->
<button type="submit">Enviar</button>             <!-- equivalente -->
```

Puntos importantes:
- 🔑 **El `name` es lo que usa PHP** para recoger el dato. El `id` no se envía.
- En un `<select>` se envía el **`value`** de la opción elegida, no el texto visible (por eso en el 2B sale `ASIR` y no el nombre largo).
- Si una `<option>` **no tiene `value`**, se envía su **texto**.
- `<fieldset>` dibuja un recuadro y `<legend>` le pone título (2B: "Resumen:").
- `<label>` asocia un texto a un control.

---

## 10. Recoger datos: `filter_input`

```php
$usuario = filter_input(INPUT_GET, "NombreUsuario");
$var1    = filter_input(INPUT_POST, "valor1");
```

- 1er parámetro: `INPUT_GET` o `INPUT_POST` (según el `method` del form).
- 2º parámetro: el **`name`** del control, **entre comillas** y **escrito exactamente igual**.

Qué devuelve:

| Situación | Valor |
|---|---|
| El campo existe y tiene texto | el texto (`"Pepe"`, `"5"`) |
| El campo existe pero está **vacío** | `""` (cadena vacía) |
| El campo **no existe** (no se envió o el `name` está mal escrito) | `null` |

Otra forma que viste en 5B: `$_POST["numero"]` / `$_GET["numero"]`. Hacen lo mismo, pero en clase se usa sobre todo `filter_input`.

---

## 11. `if / elseif / else`

```php
if (condición) {
    // si se cumple
} elseif (otra_condición) {
    // si no se cumplió la primera pero sí esta
} else {
    // si no se cumple ninguna
}
```

### Operadores de comparación

| Operador | Significado |
|---|---|
| `==` | igual |
| `!=` | distinto |
| `>` `<` | mayor / menor |
| `>=` `<=` | mayor o igual / menor o igual |

⚠️ `=` **asigna**, `==` **compara**. `if ($a = $b)` es un error (ver apartado 18).

### Operadores lógicos

| Operador | Equivalente | Significado |
|---|---|---|
| `and` | `&&` | se cumplen **las dos** |
| `or` | `\|\|` | se cumple **al menos una** |
| `!` | | **niega** (`!isset($x)` → "no existe") |

### Ejemplo: el mayor de 3 números (3A)

```php
if ($n1 > $n2 and $n1 > $n3) {
    $rdo = "El primer valor ($n1) es el mayor";
} elseif ($n2 > $n3) {           // aquí ya sé que $n1 NO es el mayor
    $rdo = "El segundo valor ($n2) es el mayor";
} else {
    $rdo = "El tercer valor ($n3) es el mayor";
}
print "<h3>$rdo</h3>";
```

> Fíjate en el truco del profe: en el `elseif` no hace falta volver a comparar con `$n1`.

También se pueden **anidar** `if` dentro de `else` (el profe lo hace en 3A y 3D). Hace lo mismo que el `elseif`.

---

## 12. Validaciones

### 12.1 Campo de texto vacío

```php
if ($nombre == "") { ... }            // vacío
if (trim($nombre) == "") { ... }      // vacío o solo espacios  ← mejor (4B profe)
```

- `trim($texto)` → quita los **espacios del principio y del final**.

### 12.2 Lista sin seleccionar

Depende del `value` que tenga la primera opción ("--- Selecciona ---"):

```html
<option value="0"> --- Selecciona nº 1 --- </option>   ← profe
```
```php
if ($n1 == 0 or $n2 == 0 or $n3 == 0) { ... }
```

o bien

```html
<option value=""> --- Selecciona nº 1 --- </option>    ← tú
```
```php
if ($n1 == "" or $n2 == "" or $n3 == "") { ... }
```

⚠️ **Sé coherente**: si el value es `""`, compara con `""`. En PHP 8, `"" == 0` es **falso**.

### 12.3 `isset` y `!`

```php
isset($x)                 // true si $x existe y NO es null
!isset($x)                // true si no existe (p.ej. el name está mal o no se envió)
isset($a, $b, $c)         // true si existen las tres
if (!$x) { ... }          // true si $x está vacío ("", "0", 0, null, false)
```

### 12.4 Valores repetidos (3B)

```php
if ($n1 == 0 or $n2 == 0 or $n3 == 0) {
    print "<h3 class='fallo'>Es necesario introducir los 3 valores</h3>";
    print "<a href='Ejercicio3B.html'>&lt;&lt;&lt; Volver</a>";
} elseif ($n1 == $n2 or $n1 == $n3 or $n2 == $n3) {
    print "<h3 class='fallo'>Valores repetidos</h3>";
    print "<a href='Ejercicio3B.html'>&lt;&lt;&lt; Volver</a>";
} elseif ($n1 > $n2 and $n1 > $n3) {
    print "El primer valor ($n1) es el mayor";
} elseif ($n2 > $n3) {
    print "El segundo valor ($n2) es el mayor";
} else {
    print "El tercer valor ($n3) es el mayor";
}
```

> Orden de comprobaciones: **1º faltan datos → 2º datos incorrectos → 3º resultado.**

### 12.5 Listar TODOS los datos que faltan (3C)

Se va **acumulando** en una variable de texto con `if` independientes (¡no `elseif`, porque pueden faltar varios!):

```php
$faltan = "";
if ($nombre == "")    { $faltan .= "Nombre, "; }
if ($ape1 == "")      { $faltan .= "Primer apellido, "; }
if ($dire == "")      { $faltan .= "Dirección, "; }
if ($cp == "")        { $faltan .= "Código postal, "; }
if ($estudios == "0") { $faltan .= "Estudios, "; }

if ($faltan != "") {
    print "<h3 class='fallo'>Faltan los siguientes datos:</h3>";
    print "<p>$faltan</p>";
} else {
    // mostrar el resumen del 2B
}
```

### 12.6 Validaciones en cascada (4B)

```php
$nombre = filter_input(INPUT_GET, "nombre");
if (trim($nombre) == "") {
    print "<h3 class='fallo'>Debes indicar tu nombre</h3>";
} else {
    // solo si hay nombre recojo y miro las notas
    $aso = filter_input(INPUT_GET, "aso");
    ...
    if ($aso == 0 or $asgbd == 0 or ...) {
        print "<h3 class='fallo'><b>$nombre :</b> Faltan notas por seleccionar</h3>";
    } else {
        // calcular media + switch
    }
}
```

---

## 13. `switch`

Compara **una variable** con muchos valores concretos.

```php
switch ($variable) {
    case valor1:
        // instrucciones
        break;
    case valor2:
        // instrucciones
        break;
    default:
        // si no coincide con ninguno
}
```

- `break` → sale del switch. **Si lo olvidas, sigue ejecutando el siguiente `case`**.
- `default` es opcional.
- El último `case` no necesita `break` (el profe no lo pone).

### Casos agrupados (4B)

```php
switch ($media) {
    case 1:
    case 2:
        print "<h3>$media -&gt; Muy Deficiente</h3>";
        break;
    case 3:  print "<h3>$media -&gt; Deficiente</h3>";   break;
    case 4:  print "<h3>$media -&gt; Insuficiente</h3>"; break;
    case 5:  print "<h3>$media -&gt; Suficiente</h3>";   break;
    case 6:  print "<h3>$media -&gt; Bien</h3>";         break;
    case 7: case 8:
        print "<h3>$media -&gt; Notable</h3>";
        break;
    case 9: case 10:
        print "<h3>$media -&gt; Sobresaliente</h3>";
}
```

### Letra del DNI (4A)

Regla: resto de `DNI / 23` → letra en este orden (T = resto 0, E = resto 22):

```
0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18 19 20 21 22
T  R  W  A  G  M  Y  F  P  D  X  B  N  J  Z  S  Q  V  H  L  C  K  E
```

```php
$resto = $dni % 23;
switch ($resto) {
    case 0:  $letra = "T"; break;
    case 1:  $letra = "R"; break;
    case 2:  $letra = "W"; break;
    // ... (así hasta el 22)
    case 22: $letra = "E";
}
$dni = $dni . "-" . $letra;     // 12345678-Z
```

> Truco para recordar el orden: **"TRWAGMYFPDXBNJZSQVHLCKE"**.
> Comprueba: 12345678 % 23 = 14 → **Z**.

---

## 14. Fecha y hora

(Ejercicio 3D – saludo según la hora)

```php
$fecha = getdate();              // devuelve la fecha/hora actual con varios datos
$hora     = $fecha["hours"];     // 0-23
$minutos  = $fecha["minutes"];   // 0-59
$segundos = $fecha["seconds"];   // 0-59
```

### `str_pad` – rellenar con ceros (para que salga `09:05:03` y no `9:5:3`)

```php
$minutos = str_pad($minutos, 2, "0", STR_PAD_LEFT);
//                 texto,  longitud mínima, carácter de relleno, por la izquierda
```

### Refrescar la página automáticamente (HTML, no PHP)

```html
<meta http-equiv="refresh" content="1;url=ejercicio3D.php">
<!-- cada 1 segundo vuelve a cargar ejercicio3D.php → el reloj "se mueve" -->
```

### Saludo según la hora

```php
if ($hora >= 0 and $hora < 7) {
    print '<h1>Deberías estar durmiendo...</h1>';
} else {
    if ($hora < 12) {
        print '<h1>¡¡ Buenos días !!</h1>';
    } elseif ($hora < 20) {
        print '<h1>¡¡ Buenas tardes!!</h1>';
    } else {
        print '<h1>¡¡ Buenas noches!!</h1>';
    }
    print "<h2> ... y buena suerte!!</h2>";   // común a los 3 → se pone una sola vez
}
print "<h3>$hora:$minutos:$segundos</h3>";
```

---

## 15. Bucles

El 5A pedía usar **los 3 tipos**, uno en cada lista. Los tres hacen lo mismo aquí (del 1 al 50):

### `for` – cuando sabes cuántas vueltas

```php
for ($i = 1; $i <= 50; $i++) {
    print "<option value='$i'>$i</option>";
}
//   inicio ; condición ; incremento
```

### `while` – comprueba ANTES de cada vuelta

```php
$i = 1;                       // inicio fuera
while ($i <= 50) {            // condición
    echo "<option value='$i'>$i</option>";
    $i += 1;                  // ¡incremento dentro o bucle infinito!
}
```

### `do … while` – comprueba DESPUÉS → se ejecuta **al menos 1 vez**

```php
$i = 1;
do {
    echo "<option value='$i'>$i</option>";
    $i += 1;
} while ($i <= 50);           // ojo al ; final
```

| | Se comprueba la condición | Mínimo de vueltas |
|---|---|---|
| `for` | antes | 0 |
| `while` | antes | 0 |
| `do…while` | **después** | **1** |

### Bucles anidados (5A opcional 1 – las 3 listas con un solo bucle)

```php
for ($lista = 1; $lista <= 3; $lista++) {
    echo "<label>Cantidad $lista:</label>";
    echo "<select name='cant$lista'>";
    echo "<option value='0'>--- Selecciona nº $lista ---</option>";
    for ($i = 1; $i <= 50; $i++) {
        echo "<option value='$i'>$i</option>";
    }
    echo "</select><br>";
}
```

> `name='cant$lista'` genera `cant1`, `cant2`, `cant3` → el PHP de resultado no cambia.

---

## 16. Patrones típicos con bucles

Todos del **5B**. Apréndelos, en el examen caen variaciones.

### Lista separada por comas SIN coma al final (5B-1)

```php
for ($i = 1; $i <= 100; $i++) {
    echo $i;
    if ($i < 100) {
        echo ", ";
    }
}
```

### Contar de 2 en 2 hacia atrás (5B-3: pares del 100 al 0)

```php
for ($i = 100; $i >= 0; $i -= 2) {
    echo $i;
    if ($i > 0) { echo ", "; }
}
```

> ⚠️ El enunciado pide **del 100 al 0**. Ojo con la condición: `$i >= 0` (no `$i <= 0`).

### Generar nombres de fichero (5B-0: galería)

```php
for ($i = 1; $i <= 14; $i++) {
    print "<p><img src='foto$i.jpg' width='500' /></p>";
    print "<p>foto$i.jpg</p>";
}
```

### Acumular texto (5B-4: triángulo con UN solo asterisco en el código)

```php
$linea = "";
for ($i = 1; $i <= 10; $i++) {
    $linea .= "*";
    print "<p>$linea</p>";
}
```

### Tabla de multiplicar (5B-2)

```php
for ($i = 1; $i <= 10; $i++) {
    $resultado = $numero * $i;
    print "<p>$numero x $i = $resultado</p>";
}
```

### Divisores (5B-6)

```php
for ($i = 1; $i <= $numero; $i++) {
    if ($numero % $i == 0) {
        echo "$i ";
    }
}
```

### Número primo con "bandera" (5B-5)

```php
$primo = true;                     // suponemos que lo es
$divisor = 2;
$raiz = sqrt($numero);
while ($divisor <= $raiz and $primo) {
    if ($numero % $divisor == 0) {
        $primo = false;            // encontrado un divisor → no es primo
    }
    $divisor++;
}
if ($primo) { print "$numero ES primo"; }
else        { print "$numero NO es primo"; }
```

> Recuerda: 0 y 1 **no** son primos (compruébalo antes).

### Fibonacci (5B-7)

```php
$anterior = 1;
$actual = 1;
echo "$anterior, $actual";
for ($i = 3; $i <= 20; $i++) {
    $siguiente = $anterior + $actual;
    echo ", $siguiente";
    $anterior = $actual;
    $actual = $siguiente;
}
// 1, 1, 2, 3, 5, 8, 13, 21, 34 ...
```

### Contador y acumulador

```php
$contador = 0;    // cuenta cuántas veces pasa algo  → $contador++;
$suma = 0;        // va sumando valores               → $suma += $i;
```

---

## 17. Formulario que se envía a sí mismo

(5B-2, 5, 6) El formulario y el resultado están en el **mismo `.php`**:

```php
<form action="ejercicio2.php" method="post">          <!-- action = el propio fichero -->
  <input type="number" name="numero">
  <input type="submit" name="enviar" value="Ver tabla">  <!-- el botón TIENE name -->
</form>

<?php
$enviar = filter_input(INPUT_POST, "enviar");
if (isset($enviar)) {               // solo si se ha pulsado el botón
    $numero = filter_input(INPUT_POST, "numero");
    // ... procesar y mostrar
}
?>
```

- La 1ª vez que se abre la página no se ha enviado nada → `$enviar` es `null` → no muestra resultado.
- Al pulsar el botón se recarga la misma página con los datos → ahora sí.

---

## 18. Errores típicos

Sacados de los propios ejercicios. **Repásalos, son los que quitan puntos**:

1. **`=` en vez de `==` en un `if`**
   ```php
   elseif ($cantidad1 = $cantidad2 || ...)   // ❌ ASIGNA, no compara
   elseif ($cantidad1 == $cantidad2 || ...)  // ✅
   ```
2. **`action` que no coincide con el nombre del fichero**: `action="resultadoA.php"` pero el fichero es `resultado2A.php` → error 404.
   En servidores Linux además importan las mayúsculas: `Ejercicio2A.php` ≠ `ejercicio2A.php`.
3. **`method` y `INPUT_...` que no coinciden**: form `method="post"` + `filter_input(INPUT_GET, ...)` → todo `null`.
4. **`name` distinto** en HTML y en PHP: `name="ape1"` vs `filter_input(..., "apellido1")`.
5. **Olvidar `break` en el `switch`** → se ejecutan los casos siguientes.
6. **Bucle infinito**: `while` sin incrementar, o `for ($i = 1; $i <= 10; $i--)`.
7. **Heredoc mal cerrado**: el identificador de cierre distinto (`RDO` / `rdo`) o con texto detrás.
8. **Comillas simples con variables**: `'Total: $total'` muestra literalmente `$total`.
9. **Concatenar con `+`** en vez de `.`.
10. **Falta `;`** al final de la instrucción (el error dice `unexpected ...` en la **línea siguiente**).
11. **Paréntesis en la media**: `$a + $b + $c / 3` ≠ `($a + $b + $c) / 3`.
12. **Comparar con el valor equivocado**: `value=""` en la opción y luego `if ($x == 0)`.
13. **No leer bien el enunciado**: "pares del **100 al 0**" (descendente), "solo un asterisco en el código", "tamaño 4 y máximo 5 caracteres" (`size="4" maxlength="5"`).

---

## 19. Chuleta final

```php
// VARIABLES
$x = 5;  $t = "texto";  $b = true;

// MOSTRAR
echo "a", "b";   print "Hola $t";   print 'sin $sustituir';   print "\$literal";

// CONCATENAR
$c = $a . " " . $b;     $c .= "más";

// HEREDOC
print <<<FIN
<p>Valor: <b>$x</b></p>
FIN;

// ARITMÉTICA
+  -  *  /  %     $i++   $i--   $i += 2   $i -= 2
round()  floor()  ceil()  (int)  sqrt()

// RECOGER
$v = filter_input(INPUT_GET, "name_del_input");    // o INPUT_POST

// COMPARAR / LÓGICOS
==  !=  >  <  >=  <=        and &&   or ||   !
isset($v)   trim($v) == ""

// IF
if (...) { } elseif (...) { } else { }

// SWITCH
switch ($v) { case 1: case 2: ...; break; default: ...; }

// BUCLES
for ($i = 1; $i <= 10; $i++) { }
$i = 1; while ($i <= 10) { ...; $i++; }
$i = 1; do { ...; $i++; } while ($i <= 10);

// FECHA
$f = getdate();  $f["hours"]  $f["minutes"]  $f["seconds"]
str_pad($m, 2, "0", STR_PAD_LEFT)
<meta http-equiv="refresh" content="1;url=pagina.php">
```

**DNI:** `TRWAGMYFPDXBNJZSQVHLCKE` · resto de `% 23`
**Notas:** 1-2 Muy deficiente · 3 Deficiente · 4 Insuficiente · 5 Suficiente · 6 Bien · 7-8 Notable · 9-10 Sobresaliente

¡Mucha suerte en el examen! 💪
