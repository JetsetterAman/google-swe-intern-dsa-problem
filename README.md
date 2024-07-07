# google-swe-intern-dsa-problem
constraints N = 10^5, -10^9 <= a[i] <=10^9
Understanding - Given an array of size “N” find the number of partitions to divide the whole array in 2 equal parts. 

Solution :- Find the total sum of array ; now find how many prefixes have their sum as sum/2.

Tot = total sum of array = should be even. 
// search for prefix [0,5,0,0,5,0]
good = 0;
for(i=1;i<=n;i++){
current_sum += b[i];
if(current_sum==Tot/2){
good++;
}
}
print(good) //3

Real Question :- Same as above but you are allowed to do maximum 1 operation. 
In that operation you can change any number to 0 
After doing it your numbers of partitions should be maximum. 
[-1,5,0,0,5,0]=> change -1 to 0 [0,5,0,0,5,0]

-> n
solve(a[]){
sum = total sum of array a
good = 0;
for(i=1;i<=n;i++){
current_sum += a[i];
if(current_sum==sum/2){
good++;
}
}
return good;
}

-> b[n+1]
tot = total sum of array
for(i=1;i<=n;i++){
  a[n+1]=b[n+1]
  a[i]=0
  q = solve(a)
  w = max(w,q);
}

TC - O(N*N)

You are trying to find how many prefixes have their sum as sum/2.
Lets say you are at index “i” ; you make b[i] = 0 
-> newsum = tot - b[i] 
Now just tell me how many prefix are there whose sum is newsum/2 tell me this in O(1) 
You can use a hashmap -> <prefix_sum,frequency> 
And hashmap[newsum/2] will tell you how many prefixes have their sum as newsum/2 in the range [1…..i-1] 
But we want the answer in the range [1…..n] we are missing [i] and [i+1…….N] 
From [i+1…..N] you just need to maintain how many suffixes have their sum is prefsum/2. Which can be done by making other hashmap which stores the detail of the back part 


Answer = hashmap[prefsum/2] [1…….i-1] + hashmap2[prefsum/2][i+1……N] + special case for [1….i] 

#include <bits/stdc++.h>

using namespace std;
typedef long long int ll;
int main() {
    
    
    ll t;
    cin>>t;
    while(t--){
        ll p = 0 ; unordered_map <ll,ll> k;
        ll n;
        cin>>n;
        ll b[n+1]={0};ll tot = 0 ;
        for(ll i=1;i<=n;i++){
            cin>>b[i];tot+=b[i];
        }ll s=0;unordered_map <ll,ll> sf;
        
        for(ll i=n;i>=1;i--){s=s+b[i];sf[s]++;
            
            
        }
        
        ll d = tot;
        for(ll i=1;i<=n;i++){
            sf[d]--;
            d = d - b[i];
            ll r = 0 ; 
            ll change = -1*(b[i]);
            ll newsum = tot + change;
            if(newsum%2==0){
                ll needsum = newsum/2;
                r = r + k[needsum];
                r = r + sf[needsum];
                //cout<<sf[needsum]<<"\n";
                
            }
            
            cout<<r<<"\n";
            
            p = p + b[i];k[p]++;
            
        }
        
        ll good = 0 ;
        if(tot%2==0){
        
        ll current_sum = 0 ; 
        for(ll i=1;i<=n-1;i++){
current_sum += b[i];
if(current_sum==tot/2){
good++;
}
}
}

cout<<good;


        
        
        
        
        
    }
    
    
    
    return 0;
}



