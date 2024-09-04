# Parcial
La versión iterativa usa un bucle for para calcular el factorial de manera progresiva, multiplicando los números desde 1 hasta el número dado.
La versión recursiva, en cambio, utiliza el concepto de recursión. La función factorial_recursive() llama a sí misma con el número menos 1 hasta que llega al caso base (n == 0), en el que devuelve 1.
Para comparar el desempeño de ambas implementaciones, podemos medir el tiempo de ejecución de cada una. En general, la versión iterativa suele ser más eficiente que la recursiva, 
especialmente para números más grandes, ya que evita la sobrecarga de las llamadas recursivas.
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
