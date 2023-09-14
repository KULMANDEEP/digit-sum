# digit-sum

#include <iostream>
#include<bits/stdc++.h>
using namespace std;
long long dp[18][2];
long long cnt(string R, int n, bool tight){
	if(tight==0){
		return pow(10, n)+0.1;
	}
	if(n==0){
		return 1;
	}
	long long num = 0;
	
	int ub = R[R.size()-n]-'0';
	for(int dig=0;dig<=ub;dig++){
		num += cnt(R, n-1, tight&(dig==ub));
	}
	return num;
}
long long solve(string &R, int n, bool tight){
	if(n==0)return 0;
	if(dp[n][tight]!=-1)return dp[n][tight];
	int ub = tight?(R[R.size()-n]-'0'):9;
	long long total=0;
	for(int dig=0;dig<=ub;dig++){
		total +=dig*cnt(R, n-1, (tight&(dig==ub)));
		total += solve(R, n-1, (tight&(dig==ub)));
	}
	return dp[n][tight]=total;
}

int main() {
	int t;
	cin>>t;
	while(t--){
		int a, b;
		cin>>a>>b;
		if(a!=0)a--;
		string L = to_string(a);
		string R = to_string(b);
		memset(dp, -1, sizeof(dp));
		long long last = solve(R, R.size(), 1);
				memset(dp, -1, sizeof(dp));

		long long first = solve(L, L.size(), 1);
		cout<<(last-first)<<endl;
	}
	return 0;
}
