# Laboratorio-4
#include <stdio.h>
#include <stdlib.h>

void finLargesLine(int **matrix, int size, int *result) {
}

void allocateMatrix(int ***matrix, int size) {
}

void fillMatrix(int **matrix, int size) {
}

void printMatrix(int **matrix, int size) {
  printf("Matriz (%dx%d) : \n", size, size);
  for(int i = 0; i < size; i++) {
    printf("%d", *(*(matrix +i) +j));
    }
    printf("\n");
  }
}

void freeMatrix(int **matrix, int size) {
  for(int i = 0; i < size; i++) { 
    free( *(matrix + i) );
    }
    free( matrix);
}

int main(vaoid) {
  int size, largestLine;
  int **matrix = NULL; 
  printf("El tamano de la secuencia de 1s mas grande es: %d\n", largestLine);
  return 0;
]
