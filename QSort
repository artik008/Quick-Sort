#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
#include <string.h>
#include <sys/stat.h>
#include <fcntl.h>

#define BUF 50                                                               // Constant for adding memory.

void QSort (int* mass, int f,int l);
void Change (int* mass,int a,int b);

int main ( int argc, char* argv[])
{

FILE* mfold = fopen(argv[1],"r");                                           //File with numbers for sorting.
FILE* mfsort = fopen(argv[2],"w+");                                         //New file with sorting numbers.
int i = 0;                                                                  //Counter
int* mass = (int*)malloc(BUF*sizeof(int));                                  //An array with sortable elements.
int N = BUF;
while (!feof(mfold)){                                                       //Create an array from first file.
    if (i==N) {mass = (int*)malloc((N+BUF)*sizeof(int));                    //
    N+=BUF;                                                                 //
    }                                                                       //
    fscanf(mfold,"%d",&mass[i]);                                            //
    i++;                                                                    //
}                                                                           //

if (i == 1) {                                                               //Check, is the file is empty. If true, then exit.
    fprintf(stderr,"%s","File is empty!\n");                                //
    exit(0);                                                                //
}                                                                           //

N = i-1;                                                                    //N - the number of elements.
QSort (mass,0,N-1);                                                         //Sort an array.

for(i = 0; i < N; i++){                                                     //Fill new file with sorting numbers from our array.
    fprintf(mfsort,"%d ",mass[i]);                                          //
}                                                                           //

free(mass);                                                                 // Free the memory.
return 0;
}

void Change (int* mass,int a,int b){                                        // Procedure for exchange elements in places.
    int p = mass[a];                                                        //
    mass[a] = mass[b];                                                      //
    mass[b] = p;                                                            //
}                                                                           //

void QSort (int* mass, int f,int l) {                                       // Sorting procedure.
        int ch;                                                             // Auxiliary variable.
        double c = (mass[f]+mass[l])/2;                                     // Choosing a support element.
        if ((l-f) < 4) {                                                    //
            c = 0;                                                          //
            for (ch = f;ch <= l; ch++) c=c+mass[ch];                        //
            c = c/(l-f+1);                                                  //
        }                                                                   //
        int a = f;                                                          // We fix the edges of the sorted array.
        int b = l;                                                          //

        while (a<b){                                                        // We exchange elements around the support so that
            while (mass[a]<c) a++;                                          // the left side were smaller and right larger.
            while (mass[b]>c) b--;                                          //
            if (a<b) {                                                      //
            Change(mass,a,b);                                               //
            a++;                                                            //
            b--;                                                            //
            }                                                               //
        }                                                                   //


        if (f<a-1) QSort(mass,f,a-1);                                       // Recursively sort the left and right parts about the support element.
        if (a!=l) QSort(mass,a,l);                                          //
}
