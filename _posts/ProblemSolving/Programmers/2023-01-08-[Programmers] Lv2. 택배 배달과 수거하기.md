---
layout: post
title:  "[Programmers] Lv2. 택배 배달과 수거하기"
date:   2023-01-08
excerpt: "[Programmers] Lv2. 택배 배달과 수거하기 문제의 풀이"
category: Programmers
problemsolving: true
posts: true
# tag:
# - Greedy
comments: true
---
* TOC
{:toc}
{: .toc }

<div class="center">
    해당 문제는 프로그래머스 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/150369" target="_blank">택배 배달과 수거하기</a>에서 풀어보실 수 있습니다.
</div>

## 생각할 포인트
### 1. 조건 하나를 추가해야했음
while(deliveryLastIndex >= 0 || pickupLastIndex >= 0) 에서 || pickupLastIndex >= 0 을 넣지 않았음.

### 2. deliveries와 pickups 배열의 원소가 모두 0인 경우 2로 출력되는 예외처리를 하지 않았음.

### 3. 같은 기능을 하는 메서드를 중복으로 구현했음.
~~~ java
public int delivery(int[] deliveries, int cap, int deliveryLastIndex)\
~~~

~~~ java
public int pickup(int[] pickups, int cap, int pickupLastIndex)
~~~
solve 메서드로 한 번에 짜면 중복 제거 및 시간 단축이 가능했음
~~~ java
public boolean isAllDeliveriesZero(int[] deliveries)
~~~
~~~ java
public boolean isAllPickupsZero(int[] pickups)
~~~
### 4. solve 메서드에서 else 키워드를 빼서 더 가독성 좋은 코드로 작성하지 못함.
~~~ java
public int solve(int[] array, int cap, int lastIndex) {
	for(int i = lastIndex; i >= 0; i--) {          
		if(cap < 0) {
			return i;
		} else if(cap >= array[i]) {
			cap -= array[i];
			array[i] = 0;                
		} else {                
			array[i] -= cap;
			return i;
		}
	}
	return -1;
}
~~~
아래와 같이 변경하니 가독성이 더 좋아짐.
~~~ java
public int solve(int[] array, int cap, int lastIndex) {
	for(int i = lastIndex; i >= 0; i--) {          
		if(cap < 0) {
			return i;
		}
		
		if(cap < array[i]) {
			array[i] -= cap;
			return i;                
		}
		
		cap -= array[i];
		array[i] = 0;           
	}
	return -1;
}
~~~

## 풀이 구현
~~~ java
public class Solution_택배배달과_수거하기 {
	/**
	 * 
	 * @author ryureka
	 * 1. 배달부분 : 최대한 cap만큼 다 싣고 오른쪽 끝에서 부터 차례로 배달.
	 * 2. 픽업부분 : 오른쪽 끝에서 부터 cap만큼 최대로 수거.
	 * 3. 둘 중 어느 쪽 끝의 인덱스 값이 더 큰지 비교해서 (큰 인덱스+1)*2를 정답에 추가.
	 *
	 * 1, 2번이 결국 같은 로직이므로 solve 메서드 하나로 구현.
	 * 
	 * 예외처리
	 * 값이 모두 0일 때 0이 출력되어야 하는데 2*(0+1) = 2가 리턴되므로
	 * deliveries와 pickups 배열에 있는 모든 숫자가 0인 경우 정답을 0으로 처리.
	 */
	class Solution {    
		public long solution(int cap, int n, int[] deliveries, int[] pickups) {
			long answer = 0;
			if(isAllZero(deliveries, pickups)) return 0;
            
			int deliveryLastIndex = getLastIndex(deliveries);
			int pickupLastIndex = getLastIndex(pickups);
			answer += 2*(Math.max(deliveryLastIndex,pickupLastIndex)+1);
            
			while(deliveryLastIndex >= 0 || pickupLastIndex >= 0) {
				deliveryLastIndex = solve(deliveries,cap,deliveryLastIndex);
				pickupLastIndex = solve(pickups,cap,pickupLastIndex);
				answer += 2*(Math.max(deliveryLastIndex,pickupLastIndex)+1);
			}
            
			return answer;
		}

		public int getLastIndex(int[] array){
			for(int i = array.length - 1; i >= 0; i--) {
				if(array[i] != 0) {
					return i;
				}
			}
			return 0;
		}

		public int solve(int[] array, int cap, int lastIndex) {
			for(int i = lastIndex; i >= 0; i--) {          
				if(cap < array[i]) {
					array[i] -= cap;                                    
				}
				return i;
                
				cap -= array[i];
				array[i] = 0;           
			}
			return -1;
		}

		public boolean isAllZero(int[] deliveries, int[] pickups) {
			return isAllNumbersZero(deliveries) && isAllNumbersZero(pickups);
		}
        
		public boolean isAllNumbersZero(int[] array) {
			for(int i = 0; i < array.length; i++) {
				int number = array[i];
				if(number != 0) {
					return false;
				}
			}
			return true;
		}
	}
}
~~~