---
title: Codeforce 1342C
description: "Codeforce 1342C math number-theory"
---

<!-- toc -->

# Codeforce 1342C Yet Another Counting Problem
Today we are gonna take a look of problem Codeforce 1342C
[Problem Link](https://codeforces.com/problemset/problem/1342/C)

> **Problem**
You are given two integers a and b, and q queries. The i-th query consists of two numbers li and ri, and the answer to it is the number of integers x such that li≤x≤ri, and $((x\mod a)\mod b)\neq((x\mod b)\mod a)$. Calculate the answer for each query.
Recall that ymodz is the remainder of the division of y by z. For example, 5mod3=2, 7mod8=7, 9mod4=1, 9mod9=0.
**Input**
The first line contains one integer t (1≤t≤100) — the number of test cases. Then the test cases follow.
The first line of each test case contains three integers a, b and q (1≤a,b≤200; 1≤q≤500).
Then q lines follow, each containing two integers li and ri (1≤li≤ri≤$10^{18}$) for the corresponding query.
**Output**
For each test case, print q integers — the answers to the queries of this test case in the order they appear.

### Idea
The queried range is too big($10^{18}$), so we can't check each number directly. There must be some math in it.
Observe that $\forall x\in\{\mathbb{N}\cup0\}$, $((x\mod a)\mod b)\neq((x\mod b)\mod a)\iff\\(((x\mod ab)\mod a)\mod b)\neq(((x\mod ab)\mod b)\mod a)$
$i.e.$ replace $x$ with $x\mod ab$.
And $ab\le40000$, so it's possible to check all $x$ where $x\le40000$ if it satisfy the condition.
As the range is composed of some range of length $ab$ and a last segment with length$<ab$.
Maintain a prefix sum array for $x$ in range $[0,ab-1]$, we can easily calculate the answer. (Note that I actually maintain prefix of $[0,2ab-1]$ since I need to calculate the number of last segment).

### Code:
```c++
#pragma GCC optimize(1)
#pragma GCC optimize(2)
#pragma GCC optimize(3)
#pragma GCC optimize("Ofast")
#pragma GCC optimize("inline")
#pragma GCC optimize("-fgcse")
#pragma GCC optimize("-fgcse-lm")
#pragma GCC optimize("-fipa-sra")
#pragma GCC optimize("-ftree-pre")
#pragma GCC optimize("-ftree-vrp")
#pragma GCC optimize("-fpeephole2")
#pragma GCC optimize("-ffast-math")
#pragma GCC optimize("-fsched-spec")
#pragma GCC optimize("unroll-loops")
#pragma GCC optimize("-falign-jumps")
#pragma GCC optimize("-falign-loops")
#pragma GCC optimize("-falign-labels")
#pragma GCC optimize("-fdevirtualize")
#pragma GCC optimize("-fcaller-saves")
#pragma GCC optimize("-fcrossjumping")
#pragma GCC optimize("-fthread-jumps")
#pragma GCC optimize("-funroll-loops")
#pragma GCC optimize("-freorder-blocks")
#pragma GCC optimize("-fschedule-insns")
#pragma GCC optimize("inline-functions")
#pragma GCC optimize("-ftree-tail-merge")
#pragma GCC optimize("-fschedule-insns2")
#pragma GCC optimize("-fstrict-aliasing")
#pragma GCC optimize("-falign-functions")
#pragma GCC optimize("-fcse-follow-jumps")
#pragma GCC optimize("-fsched-interblock")
#pragma GCC optimize("-fpartial-inlining")
#pragma GCC optimize("no-stack-protector")
#pragma GCC optimize("-freorder-functions")
#pragma GCC optimize("-findirect-inlining")
#pragma GCC optimize("-fhoist-adjacent-loads")
#pragma GCC optimize("-frerun-cse-after-loop")
#pragma GCC optimize("inline-small-functions")
#pragma GCC optimize("-finline-small-functions")
#pragma GCC optimize("-ftree-switch-conversion")
#pragma GCC optimize("-foptimize-sibling-calls")
#pragma GCC optimize("-fexpensive-optimizations")
#pragma GCC optimize("inline-functions-called-once")
#pragma GCC optimize("-fdelete-null-pointer-checks")
#include <bits/stdc++.h>
using namespace std;
#define rep(i,a,n) for(int i=a;i<n;i++)
#define per(i,a,n) for(int i=n-1;i>=a;i--)
#define pb push_back
#define mp make_pair
#define all(x) (x).begin(),(x).end()
#define fi first
#define se second
#define SZ(x) ((int)(x).size())
#define min(a,b) (((a)<(b))?(a):(b))
#define max(a,b) (((a)>(b))?(a):(b))
typedef vector<int> VI;
typedef long long ll;
typedef pair<int,int> PII;
typedef double db;
mt19937 mrand(random_device{}());
const ll mod=1000000007;
int rnd(int x){return mrand()%x;}
ll powmod(ll a,ll b){ll res=1;a%=mod;assert(b>=0);for(;b;b>>=1){if(b&1)res=res*a%mod;a=a*a%mod;}return res;}
ll gcd(ll a, ll b){return b?gcd(b,a%b):a;}
#define rank oiajgpowsdjg
const int N = 100;
int parent[N], rank[N];
inline void dsinit(int n) {for (int i = 0; i < n; i++)parent[i] = i;memset(rank, 0, sizeof rank);}
inline int dsfind(int e) {return parent[e] == e ? e : parent[e] = dsfind(parent[e]);}
inline void dsunion(int s1, int s2) {if (rank[s1] < rank[s2])swap(s1, s2);parent[s2] = s1;if (rank[s1] == rank[s2]) rank[s1]++;}
//head

int t,a,b,q,pre[80050];
ll l,r;

main(void) {
  cin.tie(0);
  ios_base::sync_with_stdio(0);
  cin>>t;while(t--){
    cin>>a>>b>>q;
    pre[0]=0;rep(i,1,2*a*b+1)pre[i]=pre[i-1]+(i%a%b!=i%b%a?1:0);
    while(q--){
      cin>>l>>r;ll ans=0;
      ans+=1ll*(r-l+1)/(1ll*(a*b))*1ll*pre[a*b-1];
      ans+=pre[(l-1)%(1ll*a*b)+(r-l+1)%(1ll*a*b)]-pre[(l-1)%(1ll*a*b)];
      cout<<ans<<' ';
    }
    cout<<'\n';
  }
  return 0;
}
```
[Submission](https://codeforces.com/contest/1342/submission/87735792)