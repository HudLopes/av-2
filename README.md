#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <time.h>
#include <pthread.h>

#define ARRAY_SIZE 1000
#define NUM_CHILDREN 5
#define NUM_POSITIONS_PER_CHILD 200

int array[ARRAY_SIZE];


void preencherArray(int array[], int tamanho)
{
    int i;
    for (i = 0; i < tamanho; i++)
    {
        array[i] = i;
    }
}

void ordenarArray(int array[], int tamanho)
{
    int i, j, temp;

    for (i = 0; i < tamanho - 1; i++)
    {
        for (j = 0; j < tamanho - 1 - i; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}

int searchNumber(int number, int start, int end, int arrayPreenchido[])
{
    int i;
    for (i = start; i <= end; i++)
    {
        //printf("array: %d - number: %d", array[i], number);
        if (arrayPreenchido[i] == number)
        {
            //printf("achou numero");
            return i + 1;
        }
    }
    return -1;
}

int retornaProcesso() {
}

int main()
{
    //int array[1000];
    //srand(time(NULL)); // Inicializa a semente do gerador de números aleatórios

    //preencherArray(array, 1000);
    //ordenarArray(array, 1000);

    int numberToSearch = 910;
    int foundPosition = -1;
    int foundProcess = 0;
    int j;
    int retornoProcessos[4];

    int array[1000];
    int i;

    // Preencher o array com os números de 1 a 1000
    for (j = 0; j < 1000; j++) {
        array[j] = j + 1;
    }

    // Criar processos filhos
    for (i = 0; i < NUM_CHILDREN; i++)
    {
        int start = i * NUM_POSITIONS_PER_CHILD;
        int end = start + NUM_POSITIONS_PER_CHILD - 1;
        int position = searchNumber(numberToSearch, start, end, array);

        if (position != -1)
        {
            printf("Processo %d encontrou o numero na posicao %d\n", i + 1, position);
            //retornoProcessos[i] = i+1;
         }


    }

    return 0;
}




=======================================================================================================================================



#include <stdio.h>
#include <time.h>

int main()
{
    time_t currentTime;
    struct tm *timeInfo;
    char timeString[9];
    char amPmString[3];
    int elapsedTime = 0;

    while (elapsedTime < 60)
    {
        system("cls");
        time(&currentTime);
        timeInfo = localtime(&currentTime);

        strftime(timeString, sizeof(timeString), "%I:%M:%S", timeInfo);
        strftime(amPmString, sizeof(amPmString), "%p", timeInfo);

        printf("Hora atual: %s %s\n", timeString, amPmString);
        sleep(1);
    }

    return 0;
}

