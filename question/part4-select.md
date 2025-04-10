1. inner join과 outer join의 차이에 관해서 말씀해주세요.

> 문진수
>
> Inner Join은 조인 컬럼 값이 동일한 조합에 한해서 결과 집합에 포함됩니다. 만약 기준 테이블에 레코드가 존재하더라도 조인 대상 테이블에 일치하는 값이 없으면 결과 집합에서 제외됩니다. 반면 Outer Join의 경우 Left, Right Outer join이 일반적으로 사용되는데 주 테이블의 레코드를 기준으로 모든 결과는 기본으로 다 포함되게 됩니다. Full Outer Join도 있는데 이는 왼쪽 집합에 존재하지만 오른쪽 집합에 존재하지 않는값, 오른쪽 집합에 존재하지만 왼쪽 집합에 존재하지 않는 값도 모두 결과 집합에 포함되어 나옵니다.

> 백명규
> 
> inner join과 outer join의 차이는 on절로 같은 값에 대해 판별을 할 때 해당 컬럼에 대해 null로 없는 경우를 허용하는가 안하는가 입니다. 
> inner join은 허용하지 않고 outer join은 허용하며 이 허용하는 쪽의 위치를 left outer join 혹은 right outer join으로 정할 수 있습니다.
> 
> ※ 진수말처럼 Inner join에서 조인 컬럼 값이 동일한 조합 한해서 라는 말이 더 깔끔한 듯. 반면에 outer join은 주 테이블 기준으로 상대편의 테이블에 데이터가 없어도 된다.
> 대신 값이 없다. 이런 식으로만 설명해도 대강 알아 들을 것 같음.

---
2. HAVING절과 WHERE 절의 차이는 무엇인가요? 
그러면 ANSI SQL에서 GROUP BY절에 없는 데이터를 HAVING 절이나 SELECT 절에 사용할 수 있나요?

> 문진수
>
> SELECT 문의 쿼리 실행 순서를 살펴보면 FROM, JOIN, WHERE, GROUP BY, HAVING, SELECT, ORDER BY로 수행됩니다. WHERE절의 경우 GROUP BY 전에 실행되며 모든 대상 테이블의 레코드에 대해서 조건이 걸립니다. 반면 HAVING은 WHERE 절에서 필터링되고 GROUP BY에 의해서 그룹핑된 데이터에 대해서 조건을 적용하게 됩니다.

> 백명규
> 
> WHERE 절과 HAVING 절의 차이를 이해하기 위해선 쿼리의 실행 순서에 관해서 알아야 합니다. 
> WHERE 절은 FROM과 JOIN절로 데이터를 가져온 뒤 집계가 일어나기 전 적용이 되고, 
> HAVING 절은 집계가 일어난 이후에 적용이 됩니다. 
> 따라서, WHERE 절에는 집계 값이 아닌 데이터에 대해서 적용이 가능하며 HAVING절에서는 집계 기준이 되는 컬럼 혹은 집계 값에 대해서 적용하여 해당하는 값을 필터링할 수 있습니다.
> 
> 또한 특정 DBMS에서는 ANSI SQL 표준이 아닌 쿼리도 지원하여 GROUP BY에 명시되지 않은 컬럼에 대해서 SELECT절이나 HAVING절에 적용이 가능한 걸로 압니다. 
> 하지만 개인적으로는 해당 ANSI 표준적용 기능을 켜고 SQL을 작성하여 다른 DB에도 적용이 가능한 쿼리를 작성하는 편입니다.
> 
> ※ 이거 외에도 만약에 WHERE 절에도 HAVING 절에도 걸 수 있는 조건이라면 WHERE 절에 걸어놓는 게 나음. 그 이유는 데이터를 조금 더 미리 줄여서 가져올 수 있음.

---
3. SELECT 절로 데이터를 조회해올 때 쿼리에서 우선 적용되는 절에 관해서 순서대로 말씀해주세요.

> 문진수
>
> SELECT 문의 쿼리 실행 순서를 살펴보면 FROM, JOIN, WHERE, GROUP BY, HAVING, SELECT, ORDER BY, LIMIT 순서로 실행됩니다.

> 백명규
> 
> 데이터를 조회해올 때 일어나는 순서에 대해 이해를 하려면 데이터를 어떻게 합치고 거르는 지 순서를 생각하면 됩니다. 
> 우선 FROM절과 JOIN을 통해 드리븐 테이블과 드라이빙 테이블을 구분하고 데이터를 가져옵니다. 
> 이후 WHERE 절을 통해 1차적으로 데이터를 거릅니다. 이후 그룹핑이 일어납니다. 
> GROUP BY 절에 대해서 처리를 한 뒤 해당 그룹핑된 데이터를 거르기 위해 HAVING 절이 적용이 됩니다. 
> 이후 데이터에 대한 정렬 과정인 ORDER BY절 최종 결과를 가져오기 위해 LIMIT 절이 적용이 되어 마지막에 필요한 만큼의 데이터를 가져옵니다.

---
4. UNION, UNION ALL, INTERSECT에 관해서 설명해주세요. ANSI SQL과 MySQL에선 각각의 절이 사용이 가능한가요?

> 문진수
>
> UNION은 SELECT로 조회한 데이터를 합치는데 중복을 제거한 후 결과가 나옵니다. UNION ALL의 경우 중복을 제거하지 않고 가져옵니다. 중복 체크가 없기에 성능상 이점이 있습니다. INTERSECT의 경우 두 집합의 교집합, 즉 같은 데이터만 가져오게 됩니다. MySQL에서는 INTERSECT가 없기 때문에 JOIN, EXISTS를 조합하여 쿼리를 작성해야 합니다.

---
5. GROUP BY에서 NULL로 처리된 데이터는 집계에서 어떻게 처리되나요?

> 문진수
>
> NULL도 하나의 값으로써 다른 값들과 동일하게 하나로 묶여서 집계됩니다.

---
6. DISTINCT에 관해서 설명해주세요. 어떤 절에 사용할 수 있고, 
DISTINCT에는 인덱스가 적용이 되나요? 그리고 ANSI SQL에서 DISTINCT는 SELECT에서 하나의 컬럼에만 설정할 수있나요?

> 문진수
>
> DISTINCT는 중복을 제거하는 역할을 하지만 결과를 정렬하지는 않습니다. SELECT 되는 전체 레코드의 조합이 유일하도록 가져오는 것이지 하나의 컬럼만 유니크하게 가져오는 것은 아닙니다.

---