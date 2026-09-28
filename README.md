# Ejercicios: Analizador de Contraseñas
Autora: Belén Ramos

Revisora: Toñi Reina

Casi nadie elige "123456" pensando que es una contraseña brillante, y sin embargo sigue siendo una de las más usadas del mundo. Este boletín propone construir, con criterios de seguridad reales, una herramienta con menú que analiza y transforma texto: detecta repeticiones sospechosas, secuencias numéricas típicas de contraseñas débiles, compara contraseñas parecidas entre sí, e incluye una conversión a **leet speak** (1337 5p34k) para quien quiera sentirse hacker por un rato.

Se necesitan **tres módulos en la misma carpeta**: `seguridad.py` (Parte 1), `seguridad_test.py` (también Parte 1, con las pruebas) y `programa.py` (Parte 2). Cada función debe incluir un docstring que documente sus parámetros y su valor de retorno.

---

## Parte 1 — El módulo de análisis (`seguridad.py`)

### Ejercicio 1: Un clasificador genérico de caracteres

Python incorpora varios métodos que permiten reconocer el tipo de un carácter sin necesidad de comprobarlo a mano: `.isupper()`, `.islower()` y `.isdigit()`, aplicados a una cadena de un solo carácter, devuelven `True` o `False` según sea mayúscula, minúscula o un dígito; y `.isalnum()` devuelve `True` si el carácter es alfanumérico (una letra o un dígito).

La función `contar_caracteres_de_tipo(texto, tipo)` debe contar cuántos caracteres de `texto` son del tipo indicado, donde `tipo` puede valer `"mayuscula"`, `"minuscula"`, `"digito"` o `"simbolo"` (cualquier carácter que no sea alfanumérico).

Ejemplo:
```python
>> contar_caracteres_de_tipo("Hola Mundo", "mayuscula")
2
```

### Ejercicio 2: Mayúsculas, minúsculas, dígitos y símbolos, sin repetir código

Las funciones `contar_mayusculas(texto)`, `contar_minusculas(texto)`, `contar_digitos(texto)` y `contar_simbolos(texto)` deben apoyarse en `contar_caracteres_de_tipo`, indicándole el tipo adecuado en cada caso, sin incluir lógica propia.

Ejemplo:
```python
>> contar_mayusculas("Hola Mundo")
2
>> contar_minusculas("Hola Mundo")
7
>> contar_digitos("Clave123")
3
>> contar_simbolos("Clave123!")
1
```

### Ejercicio 3: Repeticiones consecutivas

Una contraseña como `"aaaa1111"` es débil porque repite el mismo carácter varias veces seguidas. La función `contar_repeticiones_consecutivas(texto)` debe devolver cuántas veces aparece en el texto un carácter justo a continuación de sí mismo.

Ejemplo (`"aabbbcd"`: la `a` se repite una vez y la `b` se repite dos veces → 3 repeticiones en total):
```python
>> contar_repeticiones_consecutivas("aabbbcd")
3
```

### Ejercicio 4: Detectar secuencias numéricas

Otra debilidad típica es incluir una secuencia como `"123"` dentro de la contraseña. La función `tiene_secuencia_numerica(texto)` debe devolver `True` si en algún punto del texto aparecen tres dígitos consecutivos en orden ascendente (como en `"...123..."` o `"...789..."`), y `False` en caso contrario.

Ejemplo:
```python
>> tiene_secuencia_numerica("clave123segura")
True
>> tiene_secuencia_numerica("clave135segura")
False
```

### Ejercicio 5: ¿Cuánto se parecen dos contraseñas?

Cuando alguien cambia de contraseña, muchos sistemas comprueban que la nueva no se parezca demasiado a la anterior. La función `caracteres_en_comun_al_inicio(texto1, texto2)` debe devolver cuántos caracteres coinciden, contando desde el principio, entre `texto1` y `texto2`.

Ejemplo:
```python
>> caracteres_en_comun_al_inicio("Sevilla2023", "Sevilla2024")
10
>> caracteres_en_comun_al_inicio("Hola", "Adios")
0
```

### Ejercicio 6: Invertir un texto y comprobar palíndromos

La función `invertir_texto(texto)` debe devolver el texto escrito al revés, y `es_palindromo(texto)` debe indicar si el texto se lee igual del derecho que del revés, ignorando mayúsculas/minúsculas y espacios.

Ejemplo:
```python
>> invertir_texto("Python")
'nohtyP'
>> es_palindromo("Anita lava la tina")
True
>> es_palindromo("Rodrigo lava la tina")
False
```

### Ejercicio 7: Convertir a leet speak

La función `convertir_a_leet(texto)` debe devolver el texto sustituyendo las letras `a`, `e`, `i`, `o`, `s` (en mayúscula o minúscula) por los números `4`, `3`, `1`, `0`, `5` respectivamente, dejando el resto de caracteres sin cambios.

Ejemplo:
```python
>> convertir_a_leet("Sevilla es genial")
'53v1ll4 35 g3n14l'
```

### Ejercicio 8: Fortaleza de una contraseña

La función `calcular_fortaleza(contrasena)` debe evaluar la contraseña según seis criterios, sumando un punto por cada uno que se cumpla:

- Tiene 8 caracteres o más.
- Contiene alguna mayúscula.
- Contiene algún dígito.
- Contiene algún símbolo.
- No tiene ninguna repetición consecutiva.
- No contiene ninguna secuencia numérica ascendente.

Debe devolver `"Débil"` con 0, 1 o 2 puntos; `"Media"` con 3 o 4; y `"Fuerte"` con 5 o 6. Su lógica debe apoyarse por completo en las funciones ya construidas en los ejercicios anteriores.

Ejemplo:
```python
>> calcular_fortaleza("aaaa1111")
'Media'
>> calcular_fortaleza("Cl4ve_Segura!")
'Fuerte'
```

### Ejercicio 9: Probar el módulo de forma independiente (`seguridad_test.py`)

Las pruebas de `seguridad.py` no se incluyen en el propio módulo, sino en uno aparte, `seguridad_test.py`, que importa todo su contenido con `from seguridad import *`.

Por cada función construida en los ejercicios anteriores debe existir una función `test_...` que la llame con algún dato de ejemplo y muestre el resultado por pantalla de forma legible (indicando qué se está probando, no solo el valor devuelto). Una función `main()` debe invocar, una tras otra, todas las funciones `test_...`, y el fichero debe terminar con un bloque `if __name__ == "__main__":` que llame a `main()`.

---

## Parte 2 — El programa principal con menú (`programa.py`)

Este módulo hace uso del módulo `seguridad.py`. El menú puede agrupar varias funciones relacionadas en una misma opción.

### Ejercicio 10: Mostrar el menú

La función `mostrar_menu()` debe mostrar por pantalla estas 6 opciones, más la de salir:
```
=== ANALIZADOR DE CONTRASEÑAS ===
1. Analizar composición de un texto (mayúsculas, minúsculas, dígitos, símbolos)
2. Comprobar si un texto es palíndromo
3. Detectar debilidades (repeticiones consecutivas y secuencias numéricas)
4. Convertir un texto a leet speak
5. Calcular la fortaleza de una contraseña
6. Comparar dos contraseñas (caracteres en común al inicio)
0. Salir
```

### Ejercicio 11: Pedir una opción válida

La función `pedir_opcion_valida()` debe pedir un número de opción y seguir preguntando, sin dar el turno por terminado, hasta que se introduzca un valor entre 0 y 6.

### Ejercicio 12: Ejecutar la opción elegida

La función `ejecutar_opcion(opcion)` debe recibir una opción ya validada, pedir los datos que haga falta, y mostrar el resultado correspondiente llamando a las funciones de `seguridad.py`. Las opciones 1 y 3 piden un único texto pero deben mostrar varios resultados a la vez, mientras que la opción 6 necesita pedir dos textos en lugar de uno.

Ejemplo:
```python
>> ejecutar_opcion(1)
Texto: Hola Mundo123!
Mayúsculas: 2
Minúsculas: 7
Dígitos: 3
Símbolos: 2
```

### Ejercicio 13: El bucle principal

La función `iniciar_programa()` debe mostrar el menú, pedir una opción y ejecutarla, repitiendo este ciclo mientras la opción elegida no sea la de salir; al salir, debe despedirse con un mensaje. El fichero debe terminar con un bloque `if __name__ == "__main__":` que la ponga en marcha.

Ejemplo de una sesión completa:
```
=== ANALIZADOR DE CONTRASEÑAS ===
...
Elige una opción: 6
Primera contraseña: Sevilla2023
Segunda contraseña: Sevilla2024
Caracteres en común al principio: 10

=== ANALIZADOR DE CONTRASEÑAS ===
...
Elige una opción: 0

¡Hasta luego!
```
