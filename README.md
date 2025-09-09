public class AnalisisComplejidad {

    // ====== 2) Algoritmo XXXXXX (versión corregida) ======
    static void XXXXXX(int n){
        int x = 0; // O(1)
        for (int i = 1; i <= n; i *= 5) {          // Θ(log n)
            for (int j = 1; j <= n; j += 2) {      // Θ(n)
                x = x + j;                         // O(1)
            }
            for (int k = n; k >= 1; k /= 2) {      // Θ(log n)
                x = x + 1;                         // O(1)
            }
        }
        System.out.println("XXXXXX(" + n + ") -> x = " + x + " (esperado Θ(n log n))");
    }

    // ====== 3) Ex1 y Ex2 con buscar = O(n log n) ======
    static boolean Ex1(int[] a, int elem) {
        int pos = buscar(a, elem);     // O(n log n) una vez
        int n = a.length;
        int x = pos;
        for (int i = 0; i < n; ++i) {
            x += 2;
            for (int j = 0; j < n; ++j) {
                if (a[j] > a[pos]) {
                    x++;
                }
            }
        }
        return x > elem;
    }

    static boolean Ex2(int[] a, int elem) {
        int n = a.length;
        int x = 0;
        for (int i = 0; i < n; ++i) {
            int pos = buscar(a, elem); // O(n log n) en cada iteración -> O(n^2 log n)
            x += pos + 2;
            for (int j = 0; j < n; ++j) {
                if (a[j] > a[pos]) {
                    x++;
                }
            }
        }
        return x > elem;
    }

    /**
     * Implementación de buscar con complejidad O(n log n):
     * - copia el arreglo
     * - lo ordena (O(n log n))
     * - hace binarySearch (O(log n))
     * Nota: no modifica el arreglo original 'a'.
     */
    static int buscar(int[] a, int elem) {
        int[] b = Arrays.copyOf(a, a.length);
        Arrays.sort(b); // O(n log n)
        int pos = Arrays.binarySearch(b, elem); // O(log n)
        if (pos < 0) pos = -pos - 1; // si no está, posición de inserción
        // Aseguramos estar en rango [0, n-1]
        if (pos < 0) pos = 0;
        if (pos >= b.length) pos = b.length - 1;
        return pos;
    }

    // ====== Main para ejecutar en IntelliJ ======
    public static void main(String[] args) {
        // Prueba del algoritmo XXXXXX
        XXXXXX(1000);

        // Prueba de Ex1 vs Ex2
        int[] a = {7, 3, 5, 10, 1, 9, 4, 6, 2, 8};
        int elem = 5;
        boolean r1 = Ex1(a, elem);
        boolean r2 = Ex2(a, elem);
        System.out.println("Ex1 -> " + r1 + " (complejidad O(n^2))");
        System.out.println("Ex2 -> " + r2 + " (complejidad O(n^2 log n))");
        System.out.println("Conclusión: prefiera Ex1.");
    }
}
