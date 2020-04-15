---
title: 선택 - SQL 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640189a5a31d0c21642b037e906bd6361690a9a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300943"
---
# <a name="select---sql-command"></a>SELECT - SQL 명령
하나 이상의 테이블에서 데이터를 검색합니다.  
  
 Visual FoxPro ODBC 드라이버는 이 명령에 대한 기본 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 **드라이버 설명**을 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>인수  
  
> [!NOTE]  
>  다음 인수에서 참조되는 *하위 쿼리는*SELECT 내의 SELECT이며 괄호 안에 동봉되어야 합니다. WHERE 절에서 동일한 수준(중첩되지 않음)에 최대 두 개의 하위 쿼리를 가질 수 있습니다. (인수의 해당 섹션을 참조하십시오.) 하위 쿼리에는 여러 조인 조건이 포함될 수 있습니다.  
  
 [모두 &#124; 구별]   [*별칭*.] *Select_Item* [AS *Column_Name]**[별칭*.] *Select_Item* [as *Column_Name]...]*  
 SELECT 절은 쿼리 결과에 표시되는 필드, 상수 및 식을 지정합니다.  
  
 기본적으로 ALL은 쿼리 결과의 모든 행을 표시합니다.  
  
 DISTINCT는 쿼리 결과에서 행의 중복을 제외합니다.  
  
> [!NOTE]  
>  SELECT 절당 고유를 한 번만 사용할 수 있습니다.  
  
 *별칭*. 일치하는 항목 이름을 받을 자격이 있습니다. *Select_Item* 지정한 각 항목은 쿼리 결과의 하나의 열을 생성합니다. 둘 이상의 항목의 이름이 같은 경우 열이 중복되지 않도록 테이블 별칭과 항목 이름 앞에 마침표를 포함합니다.  
  
 *Select_Item* 쿼리 결과에 포함할 항목을 지정합니다. 항목은 다음 중 하나가 될 수 있습니다.  
  
-   FROM 절의 테이블에서 필드의 이름입니다.  
  
-   동일한 상수 값이 쿼리 결과의 모든 행에 표시되도록 지정하는 상수입니다.  
  
-   사용자 정의 함수의 이름일 수 있는 식입니다.  
  
 **SELECT를 가진 사용자 정의 함수**  
  
 SELECT 절에서 사용자 정의 함수를 사용하는 것은 분명한 이점이 있지만 다음 제한 사항도 고려해야 합니다.  
  
-   SELECT를 사용하면 이러한 사용자 정의 함수가 실행되는 속도에 따라 작업 속도가 제한될 수 있습니다. C 또는 어셈블리 언어로 작성된 API 및 사용자 정의 함수를 사용하여 사용자 정의 함수와 관련된 대용량 조작을 더 잘 수행할 수 있습니다.  
  
-   SELECT에서 호출된 사용자 정의 함수에 값을 전달하는 유일한 신뢰할 수 있는 방법은 호출될 때 함수에 전달되는 인수 목록입니다.  
  
-   FoxPro의 특정 버전에서 올바르게 작동하는 금지된 조작을 실험하고 발견하더라도 이후 버전에서 계속 작동할 것이라는 보장은 없습니다.  
  
 이러한 제한 외에도 SELECT 절에서 사용자 정의 함수를 사용할 수 있습니다. 그러나 SELECT를 사용하면 성능이 저하될 수 있습니다.  
  
 다음 필드 함수는 필드 또는 필드와 관련된 식인 선택 항목과 함께 사용할 수 있습니다.  
  
-   AVG(Select_Item)-숫자 데이터의 열을 평균합니다.*Select_Item*  
  
-   COUNT*Select_Item*( Select_Item)-열에서 선택 항목의 수를 계산합니다. COUNT(*)는 쿼리 출력의 행 수를 계산합니다.  
  
-   MIN(Select_Item)-열에서 *Select_Item* 가장 작은 값을 결정합니다.*Select_Item*  
  
-   MAX(Select_Item)-열에서 *Select_Item* 가장 큰 값을 결정합니다.*Select_Item*  
  
-   *SUM(Select_Item)-숫자*데이터의 열을 합계합니다.  
  
 필드 함수를 중첩할 수 없습니다.  
  
 as *Column_Name*  
 쿼리 출력의 열에 대한 제목을 지정합니다. 이 기능은 *Select_Item* 식이거나 필드 함수를 포함하고 열에 의미 있는 이름을 지정하려는 경우에 유용합니다. *Column_Name* 식일 수 있지만 테이블 필드 이름에 허용되지 않는 문자(예: 공백)를 포함할 수는 없습니다.  
  
 FROM [*데이터베이스 이름!]* *표* [*Local_Alias]**[데이터베이스 이름!]* *표* *[Local_Alias]...]*  
 쿼리가 검색하는 데이터가 포함된 테이블을 나열합니다. 열려 있는 테이블이 없는 경우 파일 위치를 지정할 수 있도록 Visual FoxPro가 **열기** 대화 상자를 표시합니다. 테이블을 연 후에는 쿼리가 완료된 후에도 테이블이 열린 상태로 유지됩니다.  
  
 *데이터베이스 이름!* 데이터 원본에 지정된 데이터베이스 이외의 데이터베이스 이름을 지정합니다. 데이터베이스가 데이터 원본으로 지정되지 않은 경우 테이블을 포함하는 데이터베이스 이름을 포함해야 합니다. 데이터베이스 이름 뒤와 테이블 이름 앞에 느낌표(!) 구분 기호를 포함합니다.  
  
 *Local_Alias* *표에*명명된 테이블에 대한 임시 이름을 지정합니다. 로컬 별칭을 지정하는 경우 SELECT 문 전체에서 테이블 이름 대신 로컬 별칭을 사용해야 합니다. 로컬 별칭은 Visual FoxPro 환경에 영향을 주지 않습니다.  
  
 여기서 *조인 조건* [및 *조인 조건* ...]    [및 &#124; 또는 *필터 조건* [및 &#124; 또는 *필터 조건* ...]]  
 Visual FoxPro가 쿼리 결과에 특정 레코드만 포함하도록 지시합니다. WHERE는 여러 테이블에서 데이터를 검색하는 데 필요합니다.  
  
 *Join조건은* FROM 절의 테이블을 연결하는 필드를 지정합니다. 쿼리에 두 개 이상의 테이블을 포함하는 경우 첫 번째 테이블 이후의 모든 테이블에 대해 조인 조건을 지정해야 합니다.  
  
> [!IMPORTANT]  
>  조인 조건을 만들 때 다음 정보를 고려하십시오.  
  
-   쿼리에 두 개의 테이블을 포함하고 조인 조건을 지정하지 않으면 필터 조건이 충족되는 한 첫 번째 테이블의 모든 레코드가 두 번째 테이블의 모든 레코드에 조인됩니다. 이러한 쿼리는 긴 결과를 생성할 수 있습니다.  
  
-   Visual FoxPro는 빈 필드와 일치하므로 빈 필드로 테이블을 조인할 때는 주의해야 합니다. 예를 들어, 고객에 가입하는 경우. 우편 및 송장. ZIP 및 CUSTOMER에 100개의 빈 우편 번호가 포함되어 있고 INVOICE에 400개의 빈 우편 번호가 포함된 경우 쿼리 출력에는 빈 필드에서 생성된 40,000개의 추가 레코드가 포함됩니다. **EMPTY()** 함수를 사용하여 쿼리 출력에서 빈 레코드를 제거합니다.  
  
-   AND 연산자는 여러 조인 조건을 연결해야 합니다. 각 조인 조건에는 다음과 같은 양식이 있습니다.  
  
     *필드네임1 비교 필드이름2*  
  
     *FieldName1은* 한 테이블의 필드 이름이며 *FieldName2는* 다른 테이블의 필드 이름이며 *비교는* 다음 표에 설명된 연산자 중 하나입니다.  
  
|연산자|비교|  
|--------------|----------------|  
|=|같음|  
|==|정확히 동일|  
|LIKE|SQL 좋아요|  
|<>, !=, #|같지 않음|  
|>|이상|  
|>=|이상 또는 같음|  
|<|보다 작음|  
|<=|작거나 같음|  
  
 문자열이 있는 = 연산자(=)를 사용하면 SET ANSI 설정에 따라 다르게 작동합니다. SET ANSI가 OFF로 설정되면 Visual FoxPro는 Xbase 사용자에게 익숙한 방식으로 문자열 비교를 처리합니다. SET ANSI가 ON으로 설정되면 Visual FoxPro는 문자열 비교를 위한 ANSI 표준을 따릅니다. Visual FoxPro가 문자열 비교를 수행하는 방법에 대한 자세한 내용은 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md) 및 [정확한 SET을](../../odbc/microsoft/set-exact-command.md) 참조하십시오.  
  
 *Filter조건은* 쿼리 결과에 포함하기 위해 레코드가 충족해야 하는 조건을 지정합니다. 검색어에 원하는 만큼 필터 조건을 포함하여 AND 또는 OR 연산자와 연결할 수 있습니다. NOT 연산자를 사용하여 논리식의 값을 반대로 하거나 **EMPTY()를** 사용하여 빈 필드를 확인할 수도 있습니다. *FilterCondition는* 다음 예제에서 모든 양식을 사용할 수 있습니다.  
  
 **예제 1** *필드Name1 비교 필드Name2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **예제 2** *필드 이름 비교 표현식*  
  
 `payments.amount >= 1000`  
  
 **예제 3** *필드 이름 비교* ALL *(하위 쿼리)*  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 필터 조건에 ALL이 포함된 경우 해당 레코드가 쿼리 결과에 포함되기 전에 하위 쿼리에서 생성된 모든 값에 대한 비교 조건을 충족해야 합니다.  
  
 **예제 4** *필드 이름 비교* &#124; 일부 *(하위 쿼리)*  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 필터 조건에 ANY 또는 SOME이 포함된 경우 필드는 하위 쿼리에서 생성된 값 중 하나 이상에 대한 비교 조건을 충족해야 합니다.  
  
 다음 예제에서는 필드의 값이 지정된 값 범위 내에 있는지 확인합니다.  
  
 **예 5** Start_Range *End_Range* *사이의* *필드이름* [not]  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 다음 예제에서는 하나 이상의 행이 하위 쿼리의 조건을 충족하는지 여부를 확인합니다. 필터 조건에 EXISTS가 포함되어 있으면 필터 조건이 True(True)로 평가됩니다. T.) 하위 쿼리가 빈 집합으로 평가하지 않는 한  
  
 **예제 6** [NOT] 존재 *(하위 쿼리)*  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **예 7** *필드이름* [not] *in Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 필터 조건에 IN이 포함된 경우 해당 레코드가 쿼리 결과에 포함되기 전에 필드에 값 중 하나가 포함되어야 합니다.  
  
 **예제 8** *필드 이름* [NOT] IN *(하위 쿼리)*  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 여기서 필드에는 하위 쿼리에서 반환된 값 중 하나를 포함해야 해당 레코드가 쿼리 결과에 포함됩니다.  
  
 **예 9** *필드 이름* [NOT] 좋아요 *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 이 필터 조건은 *cExpression*. 백분율 기호(%) 및 밑줄 (_ ) 와일드카드 *문자는 cExpression의*일부로 표시됩니다. 밑줄은 문자열에서 알 수 없는 단일 문자를 나타냅니다.  
  
 그룹별 *그룹열* [, *그룹열* ...]  
 하나 이상의 열의 값을 기반으로 쿼리의 행을 그룹합니다. *그룹열은* 다음 중 하나일 수 있습니다.  
  
-   일반 테이블 필드의 이름입니다.  
  
-   SQL 필드 함수를 포함하는 필드입니다.  
  
-   결과 테이블의 열 위치를 나타내는 숫자 식입니다. (가장 왼쪽 열 번호는 1입니다.)  
  
 *필터 조건* 보유  
 그룹이 쿼리 결과에 포함되도록 충족해야 하는 필터 조건을 지정합니다. 갖는 그룹 BY와 함께 사용되어야하며 AND 또는 OR 연산자가 연결하여 원하는만큼 필터 조건을 포함 할 수 있습니다. NOT을 사용하여 논리식의 값을 되돌릴 수도 있습니다.  
  
 *Filter조건은* 하위 쿼리를 포함할 수 없습니다.  
  
 GROUP BY 절이 없는 HAVING 절은 WHERE 절처럼 행동합니다. HAVING 절에서 로컬 별칭 및 필드 함수를 사용할 수 있습니다. HAVING 절에 필드 함수가 없는 경우 더 빠른 성능을 위해 WHERE 절을 사용합니다.  
  
 [유니온[모두] *선택 명령]*  
 하나의 SELECT의 최종 결과와 다른 SELECT의 최종 결과를 결합합니다. 기본적으로 UNION은 결합된 결과를 확인하고 중복 된 행을 제거합니다. 괄호를 사용하여 여러 UNION 절을 결합합니다.  
  
 ALL은 UNION이 결합된 결과에서 중복 행을 제거하지 못하게 합니다.  
  
 UNION 절은 다음 규칙을 따릅니다.  
  
-   공용 구조체를 결합하려면 UNION을 사용할 수 없습니다.  
  
-   두 SELECT 명령은 쿼리 출력에 동일한 수의 열이 있어야 합니다.  
  
-   하나의 SELECT 의 쿼리 결과의 각 열은 다른 SELECT의 해당 열과 동일한 데이터 형식 및 너비를 가져야 합니다.  
  
-   최종 SELECT만 ORDER BY 절을 가질 수 있으며, 이 절은 숫자로 출력 열을 참조해야 합니다. ORDER BY 절이 포함된 경우 전체 결과에 영향을 줍니다.  
  
 UNION 절을 사용하여 외부 조인을 시뮬레이션할 수도 있습니다.  
  
 쿼리에서 두 테이블을 조인하면 조인 필드에 일치하는 값이 있는 레코드만 출력에 포함됩니다. 상위 테이블의 레코드에 하위 테이블에 해당하는 레코드가 없는 경우 상위 테이블의 레코드가 출력에 포함되지 않습니다. 외부 조인을 사용하면 하위 테이블의 일치하는 레코드와 함께 출력의 부모 테이블에 있는 모든 레코드를 포함할 수 있습니다. Visual FoxPro에서 외부 조인을 만들려면 다음 예제와 같이 중첩된 SELECT 명령을 사용해야 합니다.  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  각 세미콜론 바로 앞에 오는 공백을 포함해야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 UNION 절 이전의 명령 섹션에서는 일치하는 값이 있는 두 테이블 모두에서 레코드를 선택합니다. 관련 송장이 없는 고객 회사는 포함되지 않습니다. UNION 절 다음 명령 섹션에서는 주문 테이블에 일치하는 레코드가 없는 고객 테이블의 레코드를 선택합니다.  
  
 명령의 두 번째 섹션에 대해서는 다음 사항에 유의하십시오.  
  
-   괄호 안의 SELECT 문이 먼저 처리됩니다. 이 문은 주문 테이블에 있는 모든 고객 번호의 선택을 만듭니다.  
  
-   WHERE 절은 주문 테이블에 없는 고객 테이블의 모든 고객 번호를 찾습니다. 명령의 첫 번째 섹션은 주문 테이블에 고객 번호가 있는 모든 회사를 제공했기 때문에 이제 고객 테이블의 모든 회사가 쿼리 결과에 포함됩니다.  
  
-   UNION에 포함된 테이블의 구조는 동일해야 하므로 두 번째 SELECT 문에는 *orders.order_id* 및 *orders.emp_id* 첫 번째 SELECT 문을 나타내는 두 자리 표시자가 있습니다.  
  
    > [!NOTE]  
    >  자리 표시자 표시는 나타내는 필드와 동일한 형식이어야 합니다. 필드가 날짜 유형인 경우 자리 표시자는 {/ / }여야 합니다. 필드가 문자 필드인 경우 자리 표시자는 빈 문자열("")이어야 합니다.  
  
 *Order_Item* 의해 주문 [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC] ...]  
 하나 이상의 열의 데이터를 기반으로 쿼리 결과를 정렬합니다. 각 *Order_Item* 쿼리 결과의 열에 해당해야 하며 다음 중 하나일 수 있습니다.  
  
-   기본 SELECT 절의 선택 항목이기도 한 FROM 테이블의 필드입니다(하위 쿼리가 아님).  
  
-   결과 테이블의 열 위치를 나타내는 숫자 식입니다. (가장 왼쪽 열은 숫자 1입니다.)  
  
 ASC는 주문 항목 또는 항목에 따라 쿼리 결과에 대한 오름차순을 지정하며 ORDER BY의 기본값입니다.  
  
 DESC는 쿼리 결과에 대한 내림차순을 지정합니다.  
  
 ORDER BY를 사용하는 주문을 지정하지 않으면 쿼리 결과가 정렬되지 않은 것으로 나타납니다.  
  
## <a name="remarks"></a>설명  
 SELECT는 다른 Visual FoxPro 명령과 마찬가지로 Visual FoxPro에 내장된 SQL 명령입니다. SELECT를 사용하여 쿼리를 제기하면 Visual FoxPro는 쿼리를 해석하고 테이블에서 지정된 데이터를 검색합니다. 명령 프롬프트 창 또는 Visual FoxPro 프로그램(다른 Visual FoxPro 명령과 마찬가지로) 내에서 SELECT 쿼리를 만들 수 있습니다.  
  
> [!NOTE]  
>  SELECT는 SET FILTER로 지정된 현재 필터 조건을 준수하지 않습니다.  
  
## <a name="driver-remarks"></a>운전자 발언  
 응용 프로그램이 ODBC SQL 문 SELECT를 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 명령에 ODBC 이스케이프 시퀀스가 포함되어 없는 한 변환 없이 명령을 Visual FoxPro SELECT 명령으로 변환합니다. ODBC 이스케이프 시퀀스에 둘러싸인 항목은 Visual FoxPro 구문으로 변환됩니다. ODBC 이스케이프 시퀀스 사용에 대한 자세한 내용은 [시간 및 날짜 함수](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) 및 Microsoft *ODBC 프로그래머 의 참조를*참조하고 [ODBC의 이스케이프 시퀀스를](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 만들기 - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [삽입 - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [설정 ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [정확한 설정](../../odbc/microsoft/set-exact-command.md)
