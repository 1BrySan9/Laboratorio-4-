# Laboratorio-4
#include <stdio.h>
#include <stdlib.h>

//_________________________________________________________________________________________________

void finLargesLine(int **matrix, int size, int *result) {
#include <time.h> //Al igual que en lab 3, permite tomar el tiempo del PC
                 //como semilla para crear una matriz aleatoria
void finLargesLine(int **matrix, int size, int *result) {
//esta funcion debe buscar la linea mas larga en el segundo puntero
        int actual = 0;
        int maximo = 0;
//este par de funciones ayudan para crear un intervalo
        int *ptr = *(matrix + 0); //en adelante, ptr significa puntero
                          //el * indica que esta en primer nivel de puntero
//se requiere un ciclo que permita analizar los elementos de cada linea
        for(int i = 0; i < size * size; i++) {
                if(*(ptr + i) == 1) {
                        actual++;
                }
//este if busca que cada elemento en la linea sea 1 para seguir al siguiente elemento
//si el elemento es 1, aumenta el conteo de actual, es decir, el conteo de 1s. 
                if(actual > maximo) {
                        maximo = actual;
//El valor maximo se actualiza con cada vez que el if anterior lo hace
//Si el if anterior no se cumple, todo se detiene, evitando un bucle infinito
                }
                else {
                        actual = 0;
                }
        }
        *result = maximo;
//El resultado debe enviarse a la base de datos en primer nivel
}

//_________________________________________________________________________________________________

void allocateMatrix(int ***matrix, int size) {
        *matrix = malloc(size * sizeof(int *)); //esta linea permitira definir una cantidad de punteros
        if(*matrix == NULL){
                printf("Error al reservar memoria \n");
                exit(EXIT_FAILURE); //esto se implementa para que no genere memoria basura
        }
        int *data = malloc(size * size * sizeof(int)); //esta linea permite definir los espacios en memoria 
                if(data == NULL) {
                        printf("Error al reservar memoria \n");
                        free(*matrix);
                        exit(EXIT_FAILURE);
                }
                for(int i=0; i < size; i++){
                        *(*matrix + i) = data + (i *size);//esta linea busca conectar los punteros con el analisis de filas
                }
}

//_________________________________________________________________________________________________

void fillMatrix(int **matrix, int size) {
//al igual que en el lab 3, se debe usar algo que aleatorice la seleccion de numeros, por eso el uso de rand() % 2
//ademas, por eso se requiere incluir el tiempo como forma de generar un numero aleatorio mediante <time.h>
//se usa un ciclo porque debe analizarse columna y fila, y que lo haga elemento a elemento 
        for(int i = 0; i < size; i++){
                for(int j = 0; j < size; j++){
                        *(*(matrix + i) +j) = rand() % 2; //se anida para que sea elemento a elemento 
                }
        }
}

//_________________________________________________________________________________________________

void printMatrix(int **matrix, int size) {
  printf("\nMatriz (%dx%d) : \n", size, size);//se encontro que existia un error de cara al print, faltaba un \n
  for(int i = 0; i < size; i++) {
        for(int j = 0; j < size; j++){ //se agraga la linea que lea los elementos en las filas 
                printf("%d", *(*(matrix +i) +j));
        }
    printf("\n");
  }
}
//esta funcion solo imprimira la matriz sin mayores situaciones 

//_________________________________________________________________________________________________

void freeMatrix(int **matrix, int size) {
  //for(int i = 0; i < size; i++) { esta linea se puede plantear distinto
  //lo que se quiere es "eliminar" la matriz para evitar acumulaciones de momoria inutil, es mejor pensarlo directamente como
        (void)size; //porque la medida size esta vinculada a todo lo demas, si se elimina, lo demas, ni se ejecuta
        free( *(matrix + 0));// ya que i no existe, asignar 0 evita errores
    //}
        free( matrix);
}

//_________________________________________________________________________________________________

int main(void) {
  int size, largestLine;
  int **matrix = NULL; 
  printf("El tamano de la secuencia de 1s mas grande es: %d\n", largestLine);
  return 0;
}

//_________________________________________________________________________________________________

