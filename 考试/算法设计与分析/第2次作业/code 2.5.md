```c++
#include<iostream>
#include<string.h>
#include<cmath> 
using namespace std;
string tri[1024] = {" /\\", "/__\\"};

void dfs(int n){
	int height = pow(2,n-1);
	for(int i=0;i<height;i++){
		tri[height+i]=tri[i];
		for(int j=0;j<height-1-i;j++){
			tri[height+i]+=" ";
		}
		tri[height+i]+=tri[i];
	}
	string tmp=" ";
	for(int i=0;i<height;i++){
		tmp = "";
		for(int j=1; j<=height; j++) tmp+=" ";
		tri[i] = tmp + tri[i];
	}
}

int main(){
	int n;
	cin>>n;
	for(int i=2; i<=n; i++) dfs(i);
	for(int i=0; i<=(1<<n)-1; ++i){
		cout<<tri[i]<<endl;
	}
	return 0;
}

```