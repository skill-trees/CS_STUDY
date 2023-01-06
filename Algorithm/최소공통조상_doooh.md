## 최소 공통 조상(Lowest Common Ancestor) 알고리즘

최소 공통 조상 찾는 알고리즘  
→ 두 정점이 만나는 최초 부모 정점을 찾는 것!

4와 5의 LCA는? → '2'  
4와 6의 LCA는? → '1'

![img](images/LCA.png)

해당 정점의 depth와 parent를 저장해두는 방식으로 구현하며,  
현재 그림에서의 depth는 아래와 같을 것입니다.

```markdown
[depth : 정점]
0 → 1(root 정점)
1 → 2, 3
2 → 4, 5, 6, 7
```

<br>

parent 별도 배열에 각 정점마다 가지는 부모 정점을 저장해둔다. 
```markdown
// 1 ~ 7번 정점 (root는 부모가 없기 때문에 0)
int parent[] = {0, 1, 1, 2, 2, 3, 3}
```

```java
// 두 정점의 depth 확인하기
while(true){
	if(depth가 일치)
	    if(두 정점의 parent 일치?) LCA 찾음(종료)
            else 두 정점을 자신의 parent 정점 값으로 변경
        else // depth 불일치
        // 더 depth가 깊은 정점을 해당 정점의 parent 정점으로 변경(depth가 감소됨)
}
```

### 활용
- 트리 문제에서 공통 조상을 찾아야하는 문제
- 정점과 정점 사이의 이동거리
- 방문경로를 저장해야 할 경우