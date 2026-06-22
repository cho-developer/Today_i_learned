0. 그래프란?
    : 연결돼 있는 객체(object)간의 관계를 표현하는 자료구조.
    e.g.)
    1) Tree들도 그래프의 예시.
    2) 전기회로의 소자 간 연결 상태.

1.  Graph 관련 용어
    1-1정점(vertices==vertex): 노드(node).
    1-2간선(edge): 링크(link). 노드와 노드를 잇는거.     
    1-3 인접 정점(adjacent vertex): 하나의 정점에서 edge에 의해 직접 연결된 vertex들.
    1-4 무방향 그래프의 차수(degree):하나의 vertex에 연결된 다른 vertex의 수.(vertex 각각 마다 차수 존재)
    1-5 방향 그래프의 차수(degree): 
        1>진입 차수(in-degree):외부에서 오는 edge의 수
        2>진출 차수(out-degree):외부로 가는 edge의 수
    1-6 그래프의 경로(path)
        1>무방향 그래프 에서 "정점 s로부터 정점 e까지의 경로가 있다"의 의미:s에서 출발하여 서로 연결된 간선(Edge)들을 타고 정점들을 거쳐서 최종적으로 e까지 끊어지지 않고 도달할 수 있는 연속적인 길이 존재한다
        2>단순 경로(simple path): 경로 중에서 반복되는 간선이 없는 경로.
        3> 사이클(cycle): 단순 경로의 시작 정점과 종료 정점이 동일한 경로.// >> Tree 와 Graph의 중요한 차이점. Tree는 사이클이 X. but graph는 사이클이 있어도되고 없어도 됨.
    1-7 그래프의 종류
        1> 무방향 그래프: 소괄호로 정점을 묶음. 방향이 없으므로 양방향으로 가는거임. // V(G1) = {0,1,2,3}; E(G1)= {(0,1),(2,3)}. edge에 원소 (a,b)이 있으면 자동적으로(b,a)로도 가는거임.  

        2> 방향 그래프: <>로 정점을 묶음. //E(G2)={<0,1>,<2,3>};

        3> 가중치 그래프(network): edge에 weight(cost)가 부여된것.// 

        4> 부분 그래프(subgraph): 어느 그래프를 쪼갠거.//V(S)는 V(G)의 부분집합. V(S)가 부분 그래프의 vertices 집합.

2. 그래프 ADT(Abstract Data Type)// 그래프 설계도      
    2-1 객체(object): vertex이 집합과 edge의 집합.

    2-2 연산: 
        1>create_graph()::= 그래프를 생성.
        2>init(g)::=그래프 g를 초기화.
        3>insert_vertex(g,v)::=그래프 g에 정점 v를 삽입.
        4>insert_edge(g,u,v)::=그래프 g에 간선(u,v)를 삽입.
        5>delete_vertex(g,v)::=그래프 g의 정점 v를 삭제.
        6>delete_edge(g,u,v)::그래프g의 간선(u,v)를 삭제.
        7>is_empty(g)::=그래프 g가 공백 상태인지 확인.
        8>adjacent(v)::=정점 v에 인접한 정점들의 리스트를 반환.
        9>destory_graph(g)::=그래프 g를 제거.

3. 그래프 표현 방법//컴터가  알아듣게 그래프 코딩하는 방법
    3-1 인접 행렬(adjacent matrix): vertex 개수 N에 해당하는 NxN행렬 생성. 연결되어 있으면 1. 아니면 0을 해당 행렬에 대입. //무방향 그래프는 의 행렬: 주대각이 전부0 인 대칭행렬. <->방향 그래프: 대칭or대칭X

    3-2 인접 리스트(adjacent list): 다른 vertex와 1개 이상 **연결된**vertex 개수 N만큼 리스트 생성.각 리스트는 단일 연결 리스트.

    3-3 인접 행렬 vs 인접 리스트
        1> 총 vertex는 많은데 정작 연결된 vertex가 겁나 적을때: 연결 리스트 win!

        2> 간선의 개수가  많은 경우: 연결 행렬 win!
