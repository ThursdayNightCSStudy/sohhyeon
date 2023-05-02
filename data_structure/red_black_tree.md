# Red Black Tree

자가 균형 이진 탐색 트리의 한 종류이다. 이는 자체적으로 균형을 조정한다는 점에서 AVL 이진 탐색 트리와 비슷하지만, 트리의 구조 때문에 균형을 조정하는 과정에서 트리 회전 수가 적어 AVL 트리보다 효율적이다. RB 트리의 시간 복잡도는 O(logn)이다.

## Red Black Tree 조건

- 모든 노드는 red 또는 black이다.
- 루트 노드는 black이다.
- 모든 리프 노드는 black이다.
- 노드가 red이면 그 자식 노드는 black이다. (빨간 노드가 연속으로 나올 수 없다.)
- 루트 노드에서 모든 리프 노드까지의 경로에서 만나는 black 노드의 수는 같다.

## Red Black Tree 삽입 연산

- 새로 삽입되는 노드는 모주건 red이다.
- double red가 발생하지 않기 위해 다음 두가지 전략을 사용한다.

  - Recoloring

    새로 삽인된 노드의 삼촌 노드 (부모 노드와 형제인 노드)가 red인 경우,

         - 삽입된 노드의 부모 노드, 삼촌 노드를 black으로 하고, 조부모를 red로 한다.

         - 조부모 노드가 루트 노드가 아니라면 다시 double red가 발생할 수 있다.

         - 위와 같은 상황이 발생하면 그때 다시 recoloring 또는 rotation을 수행한다.

  - rotation

    새로 삽입된 노드의 삼촌 노드가 black이거나 null인 경우,

          - 새로 삽입된 노드, 부모 노드, 조부모 노드를 오름차순으로 정렬한다.

          - 이후 중간에 위치한 노드를 부모 노드로 하고, 나머지 두 노드를 자식 노드로 만든다.

          - 부모 노드를 black으로 하고 두 자식들을 red로 한다.

## Red Black Tree 삭제 연산

- red를 삭제할때는 그냥 삭제 연산을 수행한다. (double red만 아니면 됨)

- black을 삭제할 때는 레드-블랙 트리 조건을 유지하여야 하므로, 삽입 연산때처럼 rotation을 통해 해결한다.

<br>

> ### reference

- <a href="https://hongcoding.tistory.com/178">레드 블랙 트리</a>
