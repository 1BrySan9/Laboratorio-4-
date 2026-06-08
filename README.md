# Laboratorio-4

//EJERCICIO 1
#include <stdio.h>
#include <stdlib.h>
#include <time.h> //Al igual que en lab 3, permite tomar el tiempo del PC
                 //como semilla para crear una matriz aleatoria
//_________________________________________________________________________________________________

void findLargestLine(int **matrix, int size, int *result) {
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
//este if busca que cada elemento en la linea sea 1 para seguir al siguiente elemento
//si el elemento es 1, aumenta el conteo de actual, es decir, el conteo de 1s.
                        if(actual > maximo) {
                                maximo = actual;
//El valor maximo se actualiza con cada vez que el if anterior lo hace
//Si el if anterior no se cumple, todo se detiene, evitando un bucle infinito
                        }
                }else {
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

// se agrega el siguiente bloque ya que de cara al reporte, se quiere mostrar la secuencia tal cual 
void printSequence(int **matrix, int size) {
        int *ptr = *(matrix + 0);
        printf("\nSecuencia lineal: \n");
        for(int i = 0; i < size * size; i++) {
                printf("%d", *(ptr + i));
        }
        printf("\n");
}
//para su construccion, unicamente se utilizo lo ya utilizado en este mismo laboratoria para recorrer la matriz

//_________________________________________________________________________________________________
int main(void) {
        int size; //largestLine;es mejor trabajarlo por separado para evitar errores
        int largestLine = 0;
        int **matrix = NULL; 

        srand((unsigned)time(NULL)); //esto es para tomar una semilla aleatroia usando el tiempo 

        printf("Ingrese el tamano de la matriz:");
        scanf("%d", &size); //el valor de size determiona demasiados puntos  
                           // se opta que sea el usuario quien modifique el tamaño en lugar de partir de un valor definido

        if(size <= 0){
                printf("Tamano invalido \n");
                return 1; //evitar valores que genere problemas de creacion de matrices
        }

        //ahora se llamaran a las funciones creadas con anterioridad 
        allocateMatrix(&matrix, size);
        fillMatrix(matrix, size);
        printMatrix(matrix, size);
        findLargestLine(matrix, size, &largestLine);
        printSequence(matrix, size);
        freeMatrix(matrix, size);

        printf("\nEl tamano de la secuencia de 1s mas grande es: %d\n", largestLine);
        //el mismo fallo que en lineas superiores, hacia falta un \n
        return 0;
}

//_________________________________________________________________________________________________


//EJERCICIO 2 

#include <stdio.h>
#include <stdlib.c>

//________________________________________________________________________________________________________________

unsigned char *read_pgm(const char *filename,int *width, int *height, int *max_val) {
        FILE *fp = fopen(filename, "r");
        if(fp == NULL) {
                printf("Error al abrir %s\n", filename);
                return NULL;
}
char magic[3]; //en este ejercicio no existe la restriccion del no uso de [], por eso, se puede utilizar
        fscanf(fp, "%2s", megic);

        if(magic[0] != ´P´ || magic[1] != ´2´) {
                printf("Formato no valido\n");
                fclose(fp);
                return NULL;
        }

        fscanf(fp, "%d %d", width, height);
        fscanf(fp, "%d", max_val);

        int total=(*width) * (*height);

        unsigned char *pixels = 
                malloc(total * sizeof(unsigned char));

        if(pixels == NULL) {
                fclose(fp);
                return NULL;
        }

        int value;

        for(int i = 0;i < total; i++) {
                fscanf(fp, "%d", &value);
                *(pixels + i) = (unsigned char)value;
        }

        fclose(fp);

        return pixels;
}

//________________________________________________________________________________________________________________

void apply_threshold (unsigned char *pixels, int total, int threshold) {

        for(int i = 0; i < totaal; i++) {
                if(*(pixels + i) >= threshold) {
                        *(pixels + i) = 255;
                }
                else{
                        *(pixeñs + i) = 0;
                }
        }
}
//________________________________________________________________________________________________________________

unsigned char *make_negative(unsigned char *pixels, int total) {

        unsigned char *negative = malloc(total * sizeof(unsigned char));

        if(negative == NULL) { 
                return NULL;
        }

        for(int i = 0; i < total; i++) {
                *(negative + i) ===== 255 - *(pixels + i);
        }
        return negative;
}      
//________________________________________________________________________________________________________________

void write_pgm(const char *filename, unsigned char *pixels, int width, int height, int max_val) {
        FILE *fp = fopen(filename, "w");
        if(fp == NULL) {
                printf("Error al crear %s\n", filename);
                return;
        }
        fprintf(fp, "P2\n");
        fprintf(fp, "%d %d\n", width, height);
        fprintf(fp, "%d\n", max_val);

        for(int i = 0; i < width * height; i++) {
                fprintf(fp, "%d", *(pixels + i));
                if((i + 1) % width == 0) {
                        fprintf(fp, "\n");
                }
        }
        fclose(fp);
}
//________________________________________________________________________________________________________________

void print_stats(unsigned char *original, unsigned char *thresholded, int total) {
        int blancos = 0;
        int negros = 0;

        long sume = 0;

        for(int i = 0; i < total; i++) {
                suma += *(original + i);
                if(*(thresholded + i) == 255) {
                        blancos++;
                }
                else{
                        negros++;
                }
        }

        double promedio = (double)suma / total;
        printf("\n === ESTADISTICAS ===\n");
        printf("Pixeles blancos: %d\n", blancos);
        printf("Pixeles negros: %d\n", negros);
        printf("Promedio original: %.2f\n", promedio);
}
//________________________________________________________________________________________________________________

int main(void) {
//segun lo planteado por el esqueletto, la siguiente linea arroja errores
//int width, height, max_val, threshold;
//por ello se separaron en int individuales 
        int width;
        int height;
        int max_val;
        int threshold;

        unsigned char *pixels = NULL;
        unsigned char *thresholded = NULL;
        unsigned char *negative = NULL;

        pixels = read_pgm("input.pgm", &width, &height, &max_val);

        if(pixels == NULL) {
        return 1;
        }

        int total = width * height;

        thresholded = malloc(total * sizeof(unsigned char));

        if(thresholded == NULL) { 
                free(pixels);
                return 1;
        }

        for(int i = 0; i < total; i++){
                *(thresholded + i) = *(pixels + i);
        }

        printf("Ingrese el umbral:");
        scanf("%d", &threshold);

        apply_threshold(thresholded, total, thereshold);
        negative = make_negative(thresholded, total);

        if(negative == NULL) {
                free(pixels);
                free(thresholded);
                return 1;
        }

        write_pgm("output_threshold.pgm", thresholded, width, height, 255);
        write_pgm("output_negative.pgm", negative, width, heigth, 255);
        print_stats(pixels, thresholded, total);

        free(pixels);
        free(thresholded);
        free(negative);

        return 0;
}



