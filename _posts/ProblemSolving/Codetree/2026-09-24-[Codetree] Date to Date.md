---
layout: post
title:  "[Codetree] Date to Date"
date:   2026-09-24 09:57:00
excerpt: "[Codetree] Date to Date 문제의 풀이"
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
    해당 문제는 코드트리 <a href="https://www.codetree.ai/ko/trails/complete/curated-cards/intro-date-to-date/description" target="_blank">Date to Date</a>에서 풀어보실 수 있습니다.
</div>

## 풀이1 구현
~~~ java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int m1 = sc.nextInt();
        int d1 = sc.nextInt();
        int m2 = sc.nextInt();
        int d2 = sc.nextInt();
        // Please write your code here.
                int elapsedDays = 0;

        //                                1.  2.  3.  4.  5.  6.  7.  8.  9. 10. 11. 12.
        int[] num_of_days = new int[]{0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        while(true) {
            if(m1 == m2 && d1 == d2)
                break;
        
            elapsedDays++;
            d1++;
        
            if(d1 > num_of_days[m1]) {
                m1++;
                d1 = 1;
            }
        }
        
        System.out.print(elapsedDays+1);
    }
}
~~~

## 풀이2 구현
~~~ java
import java.util.Scanner;

public class Main {
    public static int numOfDays(int m, int d) {
        // 계산 편의를 위해 각 달에 며칠이 있는지를 적어줍니다.
        int[] days = new int[]{0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        int totalDays = 0;

        // 1월부터 (m - 1)월까지는 전부 꽉 채워져 있습니다.
        for(int i = 1; i < m; i++)
            totalDays += days[i];

        // m월의 경우에는 정확히 d일만 있습니다.
        totalDays += d;

        return totalDays;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 변수를 선언하고 입력을 받습니다.
        int m1 = sc.nextInt();
        int d1 = sc.nextInt();
        int m2 = sc.nextInt();
        int d2 = sc.nextInt();

        // 결과를 출력합니다.
        System.out.println(numOfDays(m2, d2) - numOfDays(m1, d1) + 1);
    }
}
~~~