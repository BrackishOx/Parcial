# INTEGRANTES
Santiago Alejandro Cespedes
David Andres Castellanos
Diana Katerine Acosta


# 1 punto
La versión iterativa usa un bucle for para calcular el factorial de manera progresiva, multiplicando los números desde 1 hasta el número dado. la versión recursiva, en cambio, utiliza el concepto de recursión.
La función factorial_recursive() llama a sí misma con el número menos 1 hasta que llega al caso base (n == 0), en el que devuelve 1.
Para comparar el desempeño de ambas implementaciones, podemos medir el tiempo de ejecución de cada una. En general, 
la versión iterativa suele ser más eficiente que la recursiva,  especialmente para números más grandes, ya que evita la sobrecarga de las llamadas recursivas.
```
#include <stdio.h>

// Factorial en forma iterativa
int factorial_iterative(int n) {
    int result = 1;
    for (int i = 1; i <= n; i++) {
        result *= i;
    }
    return result;
}

// Factorial en forma recursiva
int factorial_recursive(int n) {
    if (n == 0) {
        return 1;
    } else {
        return n * factorial_recursive(n - 1);
    }
}

int main() {
    int n = 10;
    printf("Factorial de %d (iterativo): %d\n", n, factorial_iterative(n));
    printf("Factorial de %d (recursivo): %d\n", n, factorial_recursive(n));

    return 0;
}
```
# 2 punto

Primero se comparan las calificaciones de los estudiantes en orden descendente, utilizando la función compare g2 g1.
Si las calificaciones son iguales, se comparan los nombres de los estudiantes en orden alfabético inverso, utilizando la función compare n1 n2.
La función mappend combina los resultados de las comparaciones anteriores, de modo que el ordenamiento final se basa primero en la calificación y luego en el nombre.

En el ejemplo de uso, se define la lista de calificaciones de estudiantes studentGrades y se llama a la función sortStudents para obtener la lista ordenada, que se imprime en la salida.
Este enfoque declarativo en Haskell se enfoca en expresar "qué" se desea lograr (ordenar la lista de estudiantes) en lugar de "cómo" hacerlo, evitando la manipulación explícita de la estructura de datos.

# Enfoque imperativo python
```
def bubble_sort(students):
  n = len(students)
  for i in range(n):
      for j in range(0, n-i-1):
          if students[j][1] < students[j+1][1] or (students[j][1] == students[j+1][1] and students[j][0] > students[j+1][0]):
              students[j], students[j+1] = students[j+1], students[j]
  return students

# Ejemplo de uso
student_grades = [
  ("Juan", 85),
  ("María", 90),
  ("Pedro", 80),
  ("Ana", 90),
  ("Luis", 85)
]

sorted_students = bubble_sort(student_grades)
print(sorted_students)
```
# Enfoque Declarativo Haskell
```
import Data.List (sortBy)

sortStudents :: [(String, Int)] -> [(String, Int)]
sortStudents = sortBy (\(n1, g1) (n2, g2) -> compare g2 g1 `mappend` compare n1 n2)

-- Ejemplo de uso
studentGrades :: [(String, Int)]
studentGrades = [("Juan", 85), ("María", 90), ("Pedro", 80), ("Ana", 90), ("Luis", 85)]

main :: IO ()
main = print (sortStudents studentGrades)
```

# 3 punto
Similar al ejemplo original pero con algunas mejoras:

Uso de strdup para simplificar la asignación de memoria para strings.
Uso de memcpy para copiar las calificaciones.
Función separada calcular_memoria_usada para calcular la memoria utilizada.
Medición del tiempo de ejecución usando clock().

Gestión de memoria: En C, la gestión de memoria es manual. Usamos malloc para asignar memoria y free para liberarla. En Haskell, la gestión de memoria es automática.
Mutabilidad: En C, los datos son mutables por defecto. En Haskell, los datos son inmutables.
Manejo de errores: En C, manejamos los errores de asignación de memoria explícitamente. En Haskell, el manejo de errores es más elegante con el uso de tipos como Maybe o Either.
Rendimiento: El código C probablemente será más rápido y usará menos memoria, pero esto dependerá de la implementación específica y el caso de uso.
Seguridad: El código C es más propenso a errores como desbordamientos de búfer o fugas de memoria. Haskell proporciona más seguridad en este aspecto.
Concisión: El código Haskell es generalmente más conciso y declarativo.

Para una comparación precisa de rendimiento, necesitaríamos ejecutar ambas implementaciones en el mismo hardware con conjuntos de datos comparables. En general, esperaríamos que la versión en C sea más rápida y use menos memoria, pero la versión en Haskell sería más segura y fácil de mantener.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

typedef struct {
    char *nombre;
    char *apellido;
    unsigned int edad;
    char *ID;
    int *calificaciones;
    size_t num_calificaciones;
} Estudiante;

Estudiante *crear_estudiante(const char *nombre, const char *apellido, unsigned int edad, const char *ID, int *calificaciones, size_t num_calificaciones) {
    Estudiante *nuevo_estudiante = (Estudiante *)malloc(sizeof(Estudiante));
    
    if (nuevo_estudiante == NULL) {
        printf("Error al asignar memoria para el estudiante.\n");
        return NULL;
    }

    nuevo_estudiante->nombre = strdup(nombre);
    nuevo_estudiante->apellido = strdup(apellido);
    nuevo_estudiante->ID = strdup(ID);
    
    if (nuevo_estudiante->nombre == NULL || nuevo_estudiante->apellido == NULL || nuevo_estudiante->ID == NULL) {
        printf("Error al asignar memoria para los campos de texto.\n");
        free(nuevo_estudiante);
        return NULL;
    }

    nuevo_estudiante->edad = edad;
    nuevo_estudiante->calificaciones = (int *)malloc(num_calificaciones * sizeof(int));
    if (nuevo_estudiante->calificaciones == NULL) {
        printf("Error al asignar memoria para las calificaciones.\n");
        free(nuevo_estudiante->nombre);
        free(nuevo_estudiante->apellido);
        free(nuevo_estudiante->ID);
        free(nuevo_estudiante);
        return NULL;
    }

    memcpy(nuevo_estudiante->calificaciones, calificaciones, num_calificaciones * sizeof(int));
    nuevo_estudiante->num_calificaciones = num_calificaciones;

    return nuevo_estudiante;
}

void liberar_estudiante(Estudiante *estudiante) {
    if (estudiante != NULL) {
        free(estudiante->nombre);
        free(estudiante->apellido);
        free(estudiante->ID);
        free(estudiante->calificaciones);
        free(estudiante);
    }
}

void imprimir_estudiante(const Estudiante *estudiante) {
    if (estudiante != NULL) {
        printf("Nombre: %s %s\n", estudiante->nombre, estudiante->apellido);
        printf("Edad: %u\n", estudiante->edad);
        printf("ID: %s\n", estudiante->ID);
        printf("Calificaciones: ");
        for (size_t i = 0; i < estudiante->num_calificaciones; i++) {
            printf("%d ", estudiante->calificaciones[i]);
        }
        printf("\n");
    }
}

size_t calcular_memoria_usada(const Estudiante *estudiante) {
    return sizeof(Estudiante) + 
           (estudiante->nombre ? strlen(estudiante->nombre) + 1 : 0) + 
           (estudiante->apellido ? strlen(estudiante->apellido) + 1 : 0) + 
           (estudiante->ID ? strlen(estudiante->ID) + 1 : 0) + 
           estudiante->num_calificaciones * sizeof(int);
}

int main() {
    int calificaciones[] = {85, 90, 78};
    size_t num_calificaciones = sizeof(calificaciones) / sizeof(calificaciones[0]);

    clock_t inicio = clock();

    Estudiante *estudiante = crear_estudiante("Carlos", "Gomez", 20, "12345678", calificaciones, num_calificaciones);

    if (estudiante != NULL) {
        imprimir_estudiante(estudiante);

        size_t memoria_usada = calcular_memoria_usada(estudiante);
        printf("Memoria utilizada: %zu bytes\n", memoria_usada);

        liberar_estudiante(estudiante);
    }

    clock_t fin = clock();
    double tiempo_cpu = ((double) (fin - inicio)) / CLOCKS_PER_SEC;
    printf("Tiempo de ejecución: %f segundos\n", tiempo_cpu);

    return 0;
}
```
