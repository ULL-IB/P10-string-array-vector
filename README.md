# Práctica 10. `std::string`, `std::array`, `std::vector`

# Factor de ponderación: 8

### Objetivos
Los objetivos de esta práctica son que el alumnado:
- Sea capaz de resolver problemas sencillos en C++ usando todos los conocimientos adquiridos hasta ahora, en particular utilizando funciones y objetos de las clases `std::string`, `std::array` y `std::vector`
- Diseñe, desarrolle y utilice funciones en sus programas, haciendo que sus programas sean modulares

### Rúbrica de evaluación de esta práctica
Se señalan a continuación los aspectos más relevantes (la lista no es exhaustiva) que se tendrán en cuenta a la hora de evaluar esta práctica. Se comprobará que el alumnado:
- Conoce los conceptos expuestos en el material de referencia de esta práctica
- Ha realizado todos los ejercicios propuestos en este enunciado
- Es capaz de escribir programas simples en C++ que resuelvan problemas de complejidad similar a los que se proponen en este documento
- Hace que sus programas se estructuren en torno a diferentes funciones (sean modulares)
- Todos sus programas se estructuran en directorios diferentes, cada uno con un fichero `Makefile` que automatice su compilación
- Utiliza en todos sus programas comentarios adecuados en el formato requerido por [Doxygen](https://www.doxygen.nl/index.html)
- Acredita que es capaz de subir programas a la plataforma [Jutge](https://jutge.org/) para su evaluación
- Ha incluido un comentario de prólogo en todos los ficheros (`*.cc`, `*.h`) de sus ejercicios
- Que todos los programas que desarrolla imprimen en pantalla un mensaje indicando la finalidad del programa, así como la información que precisará del usuario para su correcta ejecución
- Hace que todos los programas que se presentan para su evaluación cumplan con los estándares definidos en la [Guía de estilo de Google para C++](https://google.github.io/styleguide/cppguide.html) 
- Utiliza siempre identificadores significativos en su programa (para constantes, variables, etc.) y no utiliza nunca identificadores de una única letra, excepto tal vez para las variables que utilice para iterar en un bucle
- Acredita que es capaz de editar ficheros remotos en su VM usando Vi
- Ha realizado todos sus ejercicios en la máquina virtual Ubuntu de la asignatura
- Demuestra que es capaz de ejecutar comandos Linux en su VM

### Material de estudio complementario
Repase de las transparencias de clase (y sus correspondientes programas de ejemplo) todos los contenidos relacionados con los objetos de tipo `std::string`, `std::array` y `std::vector`, así como el paso de parámetros a las funciones.

Estudie los siguientes apartados del [tutorial de referencia](https://www.learncpp.com/) de la asignatura:
- [7.18 — Introduction to random number generation](https://www.learncpp.com/cpp-tutorial/introduction-to-random-number-generation/)
- [4.17 — Introduction to std::string](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring/)
- [4.18 — Introduction to std::string_view](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring_view/)
- [11.16 — An introduction to std::array](https://www.learncpp.com/cpp-tutorial/an-introduction-to-stdarray/)
- [11.17 — An introduction to std::vector](https://www.learncpp.com/cpp-tutorial/an-introduction-to-stdvector/)
- [11.13 — For-each loops](https://www.learncpp.com/cpp-tutorial/for-each-loops/)

### Ejercicios
- Al realizar los ejercicios, cree dentro de su repositorio de esta práctica un directorio diferente para cada uno de los ejercicios. Asigne a cada uno de esos directorios nombres significativos
- Automatice la compilación del programa correspondiente a cada ejercicio con un fichero `Makefile` independiente para cada programa e inclúyalo en el correspondiente directorio
- Haga que todos los programas tomen su entrada por la línea de comandos y, en caso de que se ejecuten sin pasarles el número adecuado de parámetros, impriman en pantalla un mensaje indicando el modo correcto de ejecutar el programa
- El código de cada uno de los programas deberá organizarse de forma modular, es decir haciendo uso de funciones 
- Cada función deberá realizar una única tarea y hacerla correctamente 
- El identificador de una función debe reflejar claramente lo que la función hace 

1. Desarrolle un programa que incluya una función `Concatenate` que reciba por parámetro un objeto de tipo `std::vector<std::string>` y devuelva un objeto de tipo `std::string` con la *concatenación* de todos sus elementos, separados por espacios. La función `main` deberá llamar a la función usando como argumento un vector construido a partir de los argumentos obtenidos de la línea de comandos. Por ejemplo, ejecutar el programa con los argumentos `IB GII ULL` debería generar el vector `{"IB", "GII", "ULL"}` y producir a partir de él la cadena de caracteres `"IB GII ULL"`.

2. Desarrolle un programa que incluya una función cuyo prototipo sea:
    ```cpp
    std::vector<double> GenerateVector(int size, double lower, double upper);
    ```
    Esta función debe generar y devolver un vector de `size` elementos que se inicializarán con valores generados aleatoriamente en el intervalo `(lower, upper)`. Consulte para ello en [cppreference](https://en.cppreference.com/w/cpp/numeric/random/uniform_real_distribution) cómo utilizar una distribución uniforme con números reales. Una vez tenga desarrollada esa función, podría invocarla del siguiente modo (por ejemplo):
    ```cpp
    std::vector<double> my_vector{GenerateVector(30, 5.0, 10.0)};
    for (const auto& value: my_vector) {
      std::cout << "Component: " << value << std::endl;
    }
    ```
    La llamada anterior inicializa el vector `my_vector` con 30 componentes de tipo `double`, cuyos valores se generan aleatoriamente dentro el rango `(5.0, 10.0)`. A continuación, el bucle imprime los valores que se almacenan en ese vector.

3. Desarrolle un programa que incluya una función `ReduceSum` que tome como parámetro un vector de números en punto flotante y devuelva como resultado la suma de todos los valores almacenados en el vector.
    
    Utilice la función `GenerateVector()` para generar vectores y probar el funcionamiento de `ReduceSum`.
    ```
    Public test cases
    Input           Output
    1.0 1.0 1.0      3.0
    1 2 3 4 5 6     21.0
    0 0 0 0 1 0 1    2.0
    ```

4. Desarrolle un programa que incluya una función que tome como parámetro un vector y calcule los valores máximo, mínimo y promedio de todos los valores almacenados en el vector.
    
    Puesto que una función sólo puede devolver un único valor, tendrá que investigar algún mecanismo para posibilitar que la función devuelva esos tres valores (máximo, mínimo y promedio). Una posible solución sería desarrollar tres funciones diferentes, una para cada uno de los cálculos, pero eso sería ineficiente porque ello requeriría recorrer el vector tres veces, cuando el problema se puede resolver recorriendo el vector una sola vez.
    
    Investigue cómo resolver el problema utilizando el paso de parámetros por referencia para posibilitar que la función *exporte* los tres valores que calcula. Utilice la función `GenerateVector()` para generar vectores y probar el funcionamiento de su función.

5. Una forma sencilla de generar un número entero aleatorio en cualquier rango es recurriendo a la función [`std::rand`](https://en.cppreference.com/w/cpp/numeric/random/rand) de la librería `cstdlib`, que devuelve un número entero pseudo-aleatorio en el rango [0, `RAND_MAX`]. `RAND_MAX` es una constante cuyo valor depende de la versión del compilador que se use, pero se garantiza que es al menos mayor o igual que 32767.
    
    Para ajustar el valor devuelto por `std::rand` al intervalo deseado, se puede utilizar la operación *módulo* (`%`). Por ejemplo, para obtener un valor aleatorio en el intervalo `[a, b)` (`a` incluido, `b` excluido), se podría realizar la operación
    ```
    a + std::rand() % (b - a) 
    ```
    Desarrolle un programa que incluya una función (que no devuelva nada) que tome como parámetro un vector y lo desordene. Para ello, recorra el vector e intercambie cada uno de sus elementos con una posición aleatoria dentro del mismo.
    
    Si observa que su programa siempre muestra la misma permutación del vector, estudie la función [`std::srand`](https://en.cppreference.com/w/cpp/numeric/random/srand) que permite modificar la *semilla* del generador de números aleatorios de C++.
