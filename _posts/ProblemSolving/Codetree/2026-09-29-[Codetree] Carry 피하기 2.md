---
layout: post
title:  "[Codetree] Carry 피하기 2"
date:   2026-09-29 17:34:00
excerpt: "[Codetree] Carry 피하기 2 문제의 풀이"
category: Codetree
problemsolving: true
posts: true
tag:
- 자리 수 단위로 완전탐색
comments: true
---
* TOC
{:toc}
{: .toc }

<div class="center">
    해당 문제는 코드트리 <a href="https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-escaping-carry-2/description" target="_blank">Carry 피하기 2</a>에서 풀어보실 수 있습니다.
</div>

## 풀이 구현
~~~ java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        // Please write your code here.

        int max = -1;
        for(int i = 0; i < arr.length; i++) {
            for(int j = i+1; j < arr.length; j++) {
                for(int k = j+1; k < arr.length; k++) {
                    if(isNotCarry(arr[i],arr[j],arr[k])) {
                        max = Math.max(max,arr[i]+arr[j]+arr[k]);
                    }
                }
            }
        }
        System.out.println(max);
    }

    public static boolean isNotCarry(int a, int b, int c){
        while(true) {
            if(a == 0 && b == 0 && c == 0) break;            
            if(a%10+b%10+c%10 >= 10) return false;
            a /= 10;
            b /= 10;
            c /= 10;
        }
        return true;
    }
}
~~~
if(a == 0 && b == 0 && c == 0) break;를

if(a/10 == 0 && b/10 == 0 && c/10 == 0) break;라고 하여 아래 테스트케이스에서 가장 큰 자리수의 계산이 안되는 경우가 발생하였다.
~~~
3
8230
405
4050
~~~

그리고

if(a%10+b%10+c%10 >= 10) return false;를

if(a%10+b%10+c%10 > 10) return false;
라고 등호를 빼서 아래의 테스트 케이스에서 캐리가 발생하지 않았다고 판단되는 경우가 있었다.
~~~
5
1
2
3
4
5
~~~
잘못된 출력 10

맞는 출력 9
