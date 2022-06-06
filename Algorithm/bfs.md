# bfs

- Breadth First Search : 너비 우선 탐색
- 가까운 노드 부터 탐색하는 알고리즘
- 선입선출 방식인 큐 자료구조 이용
- 인접한 노드를 반복적으로 큐에 넣도록 알고리즘 작성
    - 탐색 시작 노드를 큐에 삽입하고 방문처리
    - 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입 하고 방문처리
    - 위의 과정을 더 이상 수행할 수 없을 때까지 반복
        
        ![1](https://user-images.githubusercontent.com/46683113/172125144-0f594527-2217-435d-ab83-d8a1356fc38b.jpeg)

        
        ![2](https://user-images.githubusercontent.com/46683113/172125222-dd11c6b1-82fa-4acc-a06f-ebfd21eedc06.jpeg)

        
        ![3](https://user-images.githubusercontent.com/46683113/172125272-5e60899a-282f-4526-bee9-8b64d2e6bc39.jpeg)

        


        ```python
        from collections import deque
        
        def bfs(graph, start, visited):
          queue= deque([start])
          visited[start]=True
        
          while queue:
            v=queue.popleft()
            print(v, end=' ')
            for i in graph[v]:
              if not visited[i]:
                queue.append(i)
                visited[i]=True
        
        graph=[
          [],
          [2,3,4],
          [1,7],
          [1,4,5],
          [3,5],
          [3,4],
          [7],
          [2,6,8],
          [1,7]
        ]
        
        visited=[False]*9
        
        bfs(graph,1,visited)
        ```
        
        -출처 : 이것이 취업을 위한 코딩 테스트다 with 파이썬