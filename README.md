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
