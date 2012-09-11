#include<iostream>
#include<stdio.h>
#include<string.h>
using namespace std ;
#define INF (int)1e9

long long solve(int a)
{
 if(a == 0) return 0 ;
 if(a % 2 == 0) return solve(a - 1) + __builtin_popcount(a) ;
 return ((long long)a + 1) / 2 + 2 * solve(a / 2) ;
}

long long solve(int a,int b)
{
 if(a >= 0)
 {
  long long ret = solve(b) ;
  if(a > 0) ret -= solve(a - 1) ;
  return ret ;
 }
 long long ret = (32LL * -(long long)a) - solve(~a) ;
 if(b > 0) ret += solve(b) ;
 else if(b < -1)
 {
  b++ ;
  ret -= (32LL * -(long long)b) - solve(~b) ;
 }
 return ret ;
}

int main()
{
 int runs,a,b ;
 cin >> runs ;
 while(runs--)
 {
  cin >> a >> b ;
  long long ret = solve(a,b) ;
  cout << ret << endl ;
 }
 return 0 ;
}