```c++
#include<iostream>
using namespace std;

int main(){
	int n;
	cin>>n;
	long long int sum=0;
	int flag1=0,flag2=0;
	for(int i=0;i<n;i++){
		int x;
		cin>>x;
		if(x<0){
			sum+=(-1-x);
			flag1++;
		}else if(x>0){
			sum+=(x-1);
		}else if(x==0){
			sum+=1;
			flag2++;
		}
	}
	if(flag1%2==1&&flag2==0){
		sum+=2;
	}
	cout<<sum;
	return 0;
}

```