0. 유니온 파인드
    0-1 그래프에서 연결 요소를 판별하는데 사용.
    0-2 서로소 집합(Disjoint Set)자료구조를 기반 알고리즘.(서로소 집합의 자료구조를 관리 할때 매우 유용).

1. 핵심 연산 
    find(x): 노드 x가 속한 집합의 대표(루트)를 찾음.
    union(x,y): 노드 x,y가 속한 두 집합을 하나로 합침.
    same(x,y): x,y가 같은 집합에 속하는지 확인(find(x)==find(y))
    //비유: 학급에서 같은 팀 만들때.
    처음 시작할땐 모든 학생이 혼자. 점점 학생들이 뭉치면서 각각의 팀을 형성(A,E가 같은 팀을 구성==union(A,E) ). 이때 A,E 가 같은 팀인지 궁금. find(A), find(E)를 구하여 find(A)==find(E) 인지 검사.(same(A,E)). 


2. 구현법: 노드에 해당하는 부모 노드 생성. 부모노드가 팀.
즉, 노드 두개가 같은 그룹 인지는 해당 노드들의 부모노드가 같은 값인지 확인.//단, 부모 노드가 달라보여도 find(x)의 경로 압축으로 인해 같은 팀일수도 있음.

    def find(x) 
        if parent[x]!=x
        parenet[x]=find(parent[x]) // 경로 압축
        return parent[x];

    def union(x,y)

    rootX=find(x);
    rootY=find(y);

    if rootX!=rootY;
    parent[y]=rootX;

    def saem(x,y)

    return find(x)== find(y)