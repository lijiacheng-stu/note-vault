```c++
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a,const void *b){
    return (*(int*)a - *(int*)b);
}

int canSelect(int arr[],int n,int m,int minDist){
    int count = 1;
    int lastPos = arr[0];
    for(int i=1;i < n;i++){
        if(arr[i] - lastPos >= minDist){
            count++;
            lastPos = arr[i];
            if(count >= m){
                return 1;
            }
        }
    }
    return 0;
}

int main(){
    int n,m;
    scanf("%d %d",&n,&m);
    int *arr = (int*)malloc(n*sizeof(int));
    for(int i=0;i < n;i++){
        scanf("%d",&arr[i]);
    }
    qsort(arr,n,sizeof(int),compare);
    int left = 0;
    int right = arr[n-1] - arr[0];
    int answer = 0;
    while(left <= right){
        int mid = left + (right - left) / 2;
        if(canSelect(arr,n,m,mid)){
            answer = mid;
            left = mid + 1;
        }else{
            right = mid -1;
        }
    }
    printf("%d\n",answer);
    return 0;
}

```