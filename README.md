#Problem Statement

There is a colony where there are n houses in a row. There are  some good houses(who give chocolates to beggars) ,some bad houses (who take away chocolates from the beggar) and some neutral houses(neither give chocolates nor hit the beggar). Adil, a beggar knows which are good, bad and neutral.He was forced to visit at least one house in this colony. Each house takes 1 second to visit. He has ‘t’ seconds of time where t is the number of houses in row that give the maximum number of chocolates. In this he wants to get maximum number of chocolates. He can visit houses in increasing order of chocolates(need not be in row). He cannot go back on the road of the colony(i.e., he can go only forward). Calculate maximum number of chocolates(if he cannot get chocolates) he can get.

Input 
First line consists of number of houses n (1<=n<=100000) in the colony.
Second line consists of n space separated integers (-10^5<=n<=10^5)
Output
maximum number of chocolate.


# Solution in C++

#include <bits/stdc++.h>

using namespace std;

// Creating a function to find the time 

int maxSubArraySumlength(vector<int>a, int size){
    int count=0;
    int max_so_far = INT_MIN, max_ending_here = a[0];
 
    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far <max_ending_here)
           { max_so_far = max_ending_here;
            count ++;}
    }
    return count;}

 // function to find the total count of chocolates in time t
 
int maximumsum(vector<int> arr, int n,int t){

	vector<pair<int, int> > L(n);

	int index = 0;
	for (int i : arr) {
		L[index] = { i, index };
		index++;
	}
	L[0].second = -1;
	for (int i = 1; i < n; i++) {
		for (int j = 0; j < i; j++) {
			if (arr[i] >= arr[j]
				and L[i].first <=arr[i] + L[j].first) {
				L[i].first = arr[i] + L[j].first;
				L[i].second = j;
			}
		}
	}

	int maxi = INT_MIN, currIndex, track = 0;

	for (auto p : L) {
		if (p.first > maxi) {
			maxi = p.first;
			currIndex = track;
		}
		track++;
	}

	vector<int> result;
	int prevoiusIndex;
	while (currIndex >= 0) {
		result.push_back(arr[currIndex]);
		prevoiusIndex = L[currIndex].second;
		if (currIndex == prevoiusIndex)
			break;
		currIndex = prevoiusIndex;
	}
    int numcount=0;
    int countans=0;
    t=result.size()<t?result.size():t;
	for (int i =0; i <t; i++)
		{countans+=result[i];
        }
        return countans;
}

int main(){

    int n;
    cin>>n;
    
    vector<int> arr(n);
    
    for(int i=0;i<n;i++){
        cin>>arr[i];}
	
int t=maxSubArraySumlength(arr,n);
cout<<maximumsum(arr,n,t);
}   
  
  
  
# Code for generator in C++

  #include "testlib.h"

  #include <bits/stdc++.h>

  using namespace std;

   int main(int argc, char *argv[]) {
  registerGen(argc, argv, 1);

  int n = atoi(argv[1]);
  int t = atoi(argv[2]);
   vector<int> len(n);
   cout<<n<<endl;
   for(int i=0;i<n;i++){
     if(n>0)
    len[i]=rnd.next(-100000,100000);
   }
   shuffle(len.begin()+1,len.end());
    for( int f=0;f<n;f++){
        cout<<len[f]<<" ";
    }
  return 0;
  }
