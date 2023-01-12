## 트라이(Trie)

문자열에서 검색을 빠르게 도와주는 자료구조
```markdown
정수형에서 이진탐색트리를 이용하면 시간복잡도 O(logN)
하지만, 문자열에서 적용했을 때 문자열 최대 길이가 M 이면 O(M * logN) 이 된다.

이를 해결하기 위해 Trie를 사용한다.
트라이를 활용하면 O(M) 으로 문자열 검색이 가능함.
```

ex. 예시 ) { bear, bell, bid, bull, buy, sell, stock, stop }

![img.png](Downloads/doha/CS_STUDY/Data Structure/image/Trie.png)