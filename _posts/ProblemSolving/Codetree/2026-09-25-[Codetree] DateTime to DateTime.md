---
layout: post
title:  "[Codetree] DateTime to DateTime"
date:   2026-09-25 09:19:00
excerpt: "[Codetree] DateTime to DateTime 문제의 풀이"
category: Codetree
problemsolving: true
posts: true
tag:
- 시뮬레이션
- 날짜와 시간 계산
comments: true
---
* TOC
{:toc}
{: .toc }

<div class="center">
    해당 문제는 코드트리 <a href="https://www.codetree.ai/ko/trails/complete/curated-cards/challenge-datetime-to-datetime/description" target="_blank">DateTime to DateTime</a>에서 풀어보실 수 있습니다.
</div>

## 풀이1 구현
~~~ java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int A = sc.nextInt();
        int B = sc.nextInt();
        int C = sc.nextInt();
        // Please write your code here.
        if((A==11 && B<11) || (A==11 && B==11 && C<11)) {
            System.out.println(-1);
            return;
        }

        System.out.println(A*24*60+B*60+C-11*24*60-11*60-11);
    }
}
~~~

## 풀이2 구현
~~~ java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // 변수 선언 및 입력
        int a = sc.nextInt();
        int b = sc.nextInt();
        int c = sc.nextInt();

        // 차이를 계산합니다.
        int diff = (a * 24 * 60 + b * 60 + c) - (11 * 24 * 60 + 11 * 60 + 11);

        // 출력
        if(diff < 0)
            System.out.println(-1);
        else
            System.out.println(diff);
    }
}
~~~