---
layout: post
title:  "프로그래머스 해시-완주하지 못한 선수"
categories: [algorithm]
tags: algorithm
comments: true
---

## 목적
첫 포스팅입니다. 이 글의 목적은 혼자 공부한 것을 정리하기 위한 목적이기도 하며 저의 삽질한 흔적을 보며 다른 사람들에게도 도움이 되길 바라며 글을 남깁니다. 알고리즘 카테고리에서는 기본적으로 프로그래머스 코딩테스트 연습 문제를 한 문제씩 풀게 될 것이며, 글쓴이의 전공은 인공지능이므로 기본 언어는 파이썬을 이용합니다. 허접하지만 도움이 되시길..


## 문제-완주하지 못한 선수
---

문제 설명은 간단합니다. 참가자와 완주자의 배열이 주어졌을 때, 완주하지 못한 사람을 리턴하는 문제입니다. 이 문제는 해시 자료형 카테고리에 속해있기 때문에 문제를 풀기 위한 정도 수준의 해시 자료형에 개념에 대해  잠시 정리하고 가겠습니다.


## 해시
---
해시는 데이터를 관리하고 유지하는 과정을 용이하게 하기 위한 자료구조이며 속도적으로 뛰어난 자료형입니다. 속도적으로 뛰어난 이유는 내가 예를 들어 'kidon'이 완주 목록에 속해 있는지 찾기 위해서 모든 자료를 탐색할 필요 없이 'kidon'이라는 인덱스에 접근해보면 완주 했는지 아닌지를 즉각 확인할 수 있기 때문입니다. 파이썬에서는 딕셔너리 자료형이 이 해시와 동일한 자료형입니다.

### 용어 정의
- 데이터
>  말  그대로 정리하고 싶은 데이터죠. 위 문제에서는 참가자와 완주자의 배열입니다.
- 해시 함수
> 데이터를 정해진 규칙에 따라 해시테이블에 저장하는 역할을 수행하는 녀석입니다.
- 해시 테이블
 > 해시 함수에 의해 처리된 데이터가 저장되는 장소이며, index (or key)와 value로 이루어져 있습니다. index를 입력하면 전부 탐색하지 않아도 바로 value에 접근할 수 있습니다.

## 풀이
---

처음에는 해시를 이용하지 않고 가장 직관적인 방법으로 풀어보았습니다.
<pre>
<code>
def solution(participant, completion):
    for part in participant:
        if participant.count(part) != completion.count(part):
            return part
</code>
</pre>


위 코드는 참가자의 배열이 완주자 배열을 항상 포함하기 때문에 for문을 통해 모든 참가자에 대해 Python list형의 내장함수인 count를 통해 참가자와 완료자 수를 비교했습니다. 하지만 이렇게 풀면 정답은 맞을지라도 효율성 테스트에서 탈락하게 됩니다. for문에 count의 시간 복잡도가 n이기 때문에 O(n^2)만큼의 시간 복잡도를 갖게 됩니다.

이때 해시가 필요하게 됩니다. 파이썬에는 감사하게도 해시 함수를 직접 만들 필요 없이 collections이라는 라이브러리를 제공합니다.

이를 이용한 풀이는 다음과 같습니다.
<pre>
<code>
from collections import Counter

def solution(participant, completion):
    participant_counter = Counter(participant)
    completion_counter = Counter(completion)
    for part in participant_counter.items():
        if participant_counter[part[0]] != completion_counter[part[0]]:
            return part[0]
</code>
</pre>


collections 라이브러리에는 Counter라는 함수가 있으면 이를 이용하면 배열이 주어졌을 때 각 원소를 key로 가지며 그 원소의 숫자를 value 값을 갖도록 딕셔너리를 리턴합니다.
이를 이용하면 모든 배열을 탐색하지 않고도 바로 참가자와 완주자를 비교할 수 있으니 O(N)의 시간 복잡도만으로도 정답을 도출할 수 있습니다.
