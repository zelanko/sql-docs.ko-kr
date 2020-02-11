---
title: SELECT-SQL 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85f281aefe79a09806c42e13cd771f976362d053
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67943783"
---
# <a name="select---sql-command"></a>SELECT - SQL 명령
하나 이상의 테이블에서 데이터를 검색 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원 합니다. 드라이버 관련 정보는 **드라이버 설명**을 참조 하세요.  
  
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
>  다음 인수에서 참조 되는 *하위 쿼리*는 select 내에서 select 이며 괄호로 묶어야 합니다. WHERE 절에서는 중첩 되지 않은 같은 수준에 최대 두 개의 하위 쿼리를 사용할 수 있습니다. 인수의 섹션을 참조 하십시오. 하위 쿼리에는 여러 개의 조인 조건이 포함 될 수 있습니다.  
  
 [모든 &#124; 고유]   [*Alias*.] *Select_Item* [AS *Column_Name*] [, [*Alias*.] *Select_Item* [AS *Column_Name*] ...]  
 SELECT 절은 쿼리 결과에 표시 되는 필드, 상수 및 식을 지정 합니다.  
  
 기본적으로 모든 행이 쿼리 결과에 표시 됩니다.  
  
 DISTINCT는 쿼리 결과에서 중복 행을 제외 합니다.  
  
> [!NOTE]  
>  SELECT 절 마다 한 번만 DISTINCT를 사용할 수 있습니다.  
  
 *별칭*. 일치 항목 이름을 한정 합니다. *Select_Item* 지정 하는 각 항목은 쿼리 결과의 한 열을 생성 합니다. 두 개 이상의 항목에 동일한 이름이 있는 경우 열이 중복 되지 않도록 테이블 별칭과 항목 이름 앞에 마침표를 포함 합니다.  
  
 *Select_Item* 는 쿼리 결과에 포함할 항목을 지정 합니다. 항목은 다음 중 하나일 수 있습니다.  
  
-   FROM 절에 있는 테이블의 필드 이름입니다.  
  
-   쿼리 결과의 모든 행에 동일한 상수 값을 표시 하도록 지정 하는 상수입니다.  
  
-   사용자 정의 함수의 이름일 수 있는 식입니다.  
  
 **SELECT를 사용 하는 사용자 정의 함수**  
  
 SELECT 절에서 사용자 정의 함수를 사용 하면 명백한 이점이 있지만 다음과 같은 제한 사항도 고려해 야 합니다.  
  
-   SELECT를 사용 하 여 수행 되는 작업의 속도는 이러한 사용자 정의 함수가 실행 되는 속도에 따라 제한 될 수 있습니다. 사용자 정의 함수를 포함 하는 고용량 조작은 C 또는 어셈블리 언어로 작성 된 API 및 사용자 정의 함수를 사용 하 여 보다 효율적으로 수행할 수 있습니다.  
  
-   SELECT에서 호출 되는 사용자 정의 함수에 값을 전달 하는 신뢰할 수 있는 유일한 방법은 호출 될 때 함수에 전달 되는 인수 목록입니다.  
  
-   특정 버전의 FoxPro에서 올바르게 작동 하는 금지 된 조작을 실험 하 고 검색 하는 경우에도 이후 버전에서 계속 작동 하는 보장은 없습니다.  
  
 이러한 제한과 별도로 사용자 정의 함수는 SELECT 절에서 허용 됩니다. 그러나 SELECT를 사용 하면 성능이 저하 될 수 있다는 점에 주의 해야 합니다.  
  
 필드 또는 필드를 포함 하는 식인 select 항목에 사용할 수 있는 필드 함수는 다음과 같습니다.  
  
-   AVG (*Select_Item*)-숫자 데이터 열의 평균을 계산 합니다.  
  
-   COUNT (*Select_Item*)-열에서 선택 항목의 수를 셉니다. COUNT (*)는 쿼리 출력의 행 수를 계산 합니다.  
  
-   MIN (*Select_Item*)-열에서 *Select_Item* 의 가장 작은 값을 결정 합니다.  
  
-   MAX (*Select_Item*)-열에서 *Select_Item* 의 가장 큰 값을 결정 합니다.  
  
-   합계 (*Select_Item*)-숫자 데이터의 열 합계입니다.  
  
 필드 함수는 중첩할 수 없습니다.  
  
 AS *Column_Name*  
 쿼리 출력에서 열의 머리글을 지정 합니다. 이는 *Select_Item* 식 이거나 field 함수를 포함 하 고 열에 의미 있는 이름을 지정 하려는 경우에 유용 합니다. *Column_Name* 는 식이 될 수 있지만 테이블 필드 이름에 허용 되지 않는 문자 (예: 공백)를 포함할 수 없습니다.  
  
 FROM [*DatabaseName*!] *테이블* [*Local_Alias*] [, [*DatabaseName*!] *테이블* [*Local_Alias*] ...]  
 쿼리에서 검색 하는 데이터가 포함 된 테이블을 나열 합니다. 열려 있는 테이블이 없으면 Visual FoxPro는 파일 위치를 지정할 수 있도록 **열기** 대화 상자를 표시 합니다. 테이블이 열린 후에는 쿼리가 완료 된 후에도 테이블이 열린 상태로 유지 됩니다.  
  
 *DatabaseName*! 데이터 원본에 지정 된 데이터베이스 이외의 데이터베이스 이름을 지정 합니다. 데이터베이스를 데이터 원본으로 지정 하지 않은 경우 테이블이 포함 된 데이터베이스의 이름을 포함 해야 합니다. 데이터베이스 이름과 테이블 이름 앞에 느낌표 (!) 구분 기호를 포함 합니다.  
  
 *Local_Alias* *테이블*에서 이름이 지정 된 테이블의 임시 이름을 지정 합니다. 로컬 별칭을 지정 하는 경우 SELECT 문 전체에서 테이블 이름 대신 로컬 별칭을 사용 해야 합니다. 로컬 별칭은 Visual FoxPro 환경에 영향을 주지 않습니다.  
  
 WHERE *joincondition* [및 *joincondition* ...]    [AND &#124; 또는 *filtercondition* [및 &#124; 또는 *filtercondition* ...]]  
 는 쿼리 결과에 특정 레코드만 포함 하도록 Visual FoxPro에 지시 합니다. 는 여러 테이블에서 데이터를 검색 하는 데 필요 합니다.  
  
 *Joincondition* 은 from 절의 테이블을 연결 하는 필드를 지정 합니다. 쿼리에 둘 이상의 테이블을 포함 하는 경우 첫 번째 이후에 모든 테이블에 대 한 조인 조건을 지정 해야 합니다.  
  
> [!IMPORTANT]  
>  조인 조건을 만들 때 다음 정보를 고려 하십시오.  
  
-   쿼리에 두 개의 테이블을 포함 하 고 조인 조건을 지정 하지 않으면 첫 번째 테이블의 모든 레코드는 필터 조건이 충족 되는 한 두 번째 테이블의 모든 레코드에 조인 됩니다. 이러한 쿼리는 긴 결과를 생성할 수 있습니다.  
  
-   Visual FoxPro는 빈 필드와 일치 하므로 빈 필드가 있는 테이블을 조인 하는 경우 주의 해야 합니다. 예를 들어 고객에 게 참여 하는 경우입니다. ZIP 및 청구서. ZIP 및 고객에 게 100 빈 우편 번호가 포함 되어 있고 청구서에 400 빈 우편 번호가 포함 된 경우 쿼리 출력에는 빈 필드에서 생성 된 4만 추가 레코드가 포함 됩니다. **빈 ()** 함수를 사용 하 여 쿼리 출력에서 빈 레코드를 제거 합니다.  
  
-   여러 조인 조건을 연결 하려면 AND 연산자를 사용 해야 합니다. 각 조인 조건에는 다음과 같은 형식이 있습니다.  
  
     *FieldName1 비교 FieldName2*  
  
     *FieldName1* 는 한 테이블의 필드 이름이 고, *FieldName2* 는 다른 테이블의 필드 이름입니다. *비교* 는 다음 표에 설명 된 연산자 중 하나입니다.  
  
|연산자|비교|  
|--------------|----------------|  
|=|같음|  
|==|정확히 같음|  
|LIKE|SQL LIKE|  
|<>,! =, #|다음과 같지 않음|  
|>|다음 보다 큼|  
|>=|다음 보다 크거나 같음|  
|<|보다 작음|  
|<=|작거나 같음|  
  
 문자열에 = 연산자를 사용 하는 경우 SET ANSI의 설정에 따라 다르게 작동 합니다. SET ANSI가 OFF로 설정 된 경우 Visual FoxPro는 Xbase 사용자에 게 친숙 한 방식으로 문자열 비교를 처리 합니다. SET ANSI가 ON으로 설정 된 경우 Visual FoxPro는 문자열 비교를 위한 ANSI 표준을 따릅니다. Visual FoxPro에서 문자열 비교를 수행 하는 방법에 대 한 자세한 내용은 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md) 및 [정확히 설정](../../odbc/microsoft/set-exact-command.md) 을 참조 하세요.  
  
 *Filtercondition* 은 레코드가 쿼리 결과에 포함 되기 위해 충족 해야 하는 조건을 지정 합니다. 쿼리에서 원하는 수 만큼 필터 조건을 포함 하 여 AND 또는 OR 연산자를 사용 하 여 연결할 수 있습니다. NOT 연산자를 사용 하 여 논리 식의 값을 반대로 하거나 **empty ()** 를 사용 하 여 빈 필드를 확인할 수도 있습니다. *Filtercondition* 은 다음 예제에서 모든 폼을 사용할 수 있습니다.  
  
 **예제 1** *FieldName1 비교 FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **예제 2** *FieldName 비교 식*  
  
 `payments.amount >= 1000`  
  
 **예제 3** *FieldName Comparison* ALL (*하위 쿼리*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 필터 조건에 모두 포함 된 경우 해당 레코드는 쿼리 결과에 포함 되기 전에 하위 쿼리에서 생성 된 모든 값에 대 한 비교 조건을 충족 해야 합니다.  
  
 **예제 4** *FieldName COMPARISON* ANY &#124; SOME (*하위 쿼리*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 필터 조건에 하나 또는 일부를 포함 하는 경우 필드는 하위 쿼리에서 생성 된 하나 이상의 값에 대 한 비교 조건을 충족 해야 합니다.  
  
 다음 예제에서는 필드의 값이 지정 된 값 범위 내에 있는지 확인 합니다.  
  
 **예 5** *FieldName* [NOT] *Start_Range* 와 *End_Range* 사이  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 다음 예에서는 하나 이상의 행이 하위 쿼리의 조건을 충족 하는지 확인 합니다. 필터 조건이 있는 경우 필터 조건은 True ()로 평가 됩니다. T.)는 하위 쿼리가 빈 집합으로 계산 되지 않는 경우  
  
 **예 6** [NOT] Exists (*하위 쿼리*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 *VALUE_SET* 의 **예제 7** *FieldName* [NOT]  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 에 필터 조건이 포함 된 경우 해당 레코드는 쿼리 결과에 포함 되기 전에 필드에 값 중 하나를 포함 해야 합니다.  
  
 **예 8** *FieldName* [NOT] IN (*하위 쿼리*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 여기서 필드는 쿼리가 쿼리 결과에 포함 되기 전에 하위 쿼리에서 반환 되는 값 중 하나를 포함 해야 합니다.  
  
 **예 9** *FieldName* [NOT] *cexpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 이 필터 조건은 *Cexpression*과 일치 하는 각 필드를 검색 합니다. 백분율 기호 (%)를 사용할 수 있습니다. 및 밑줄 (_) 와일드 카드 *문자를 포함 합니다.* 밑줄은 문자열에서 알 수 없는 단일 문자를 나타냅니다.  
  
 *Groupcolumn* [, *groupcolumn* ...] 별 그룹화  
 하나 이상의 열에 있는 값을 기반으로 쿼리에서 행을 그룹화 합니다. *Groupcolumn* 은 다음 중 하나일 수 있습니다.  
  
-   일반 테이블 필드의 이름입니다.  
  
-   SQL 필드 함수를 포함 하는 필드입니다.  
  
-   결과 테이블에서 열의 위치를 나타내는 숫자 식입니다. (맨 왼쪽 열 번호는 1입니다.)  
  
 *Filtercondition*  
 그룹이 쿼리 결과에 포함 되기 위해 충족 해야 하는 필터 조건을 지정 합니다. HAVING은 GROUP BY와 함께 사용 해야 하며, AND 또는 OR 연산자를 사용 하 여 연결 하는 것과 같이 원하는 수의 필터 조건을 포함할 수 있습니다. 또한 NOT을 사용 하 여 논리 식의 값을 되돌릴 수 있습니다.  
  
 *Filtercondition* 에는 하위 쿼리를 포함할 수 없습니다.  
  
 GROUP BY 절이 없는 HAVING 절은 WHERE 절 처럼 동작 합니다. HAVING 절에서 로컬 별칭과 필드 함수를 사용할 수 있습니다. HAVING 절에 field 함수를 포함 하지 않는 경우에는 성능 향상을 위해 WHERE 절을 사용 합니다.  
  
 [UNION [ALL] *SELECTCommand*]  
 한 SELECT의 최종 결과를 다른 SELECT의 최종 결과와 결합 합니다. 기본적으로 UNION은 결합 된 결과를 확인 하 고 중복 행을 제거 합니다. 여러 UNION 절을 결합 하려면 괄호를 사용 합니다.  
  
 ALL은 UNION이 결합 된 결과에서 중복 행을 제거 하는 것을 방지 합니다.  
  
 UNION 절은 다음 규칙을 따릅니다.  
  
-   UNION을 사용 하 여 하위 쿼리를 결합할 수 없습니다.  
  
-   두 SELECT 명령의 쿼리 출력에 동일한 수의 열이 있어야 합니다.  
  
-   한 SELECT의 쿼리 결과에 있는 각 열은 다른 SELECT의 해당 열과 데이터 형식 및 너비가 동일 해야 합니다.  
  
-   최종 SELECT에는 ORDER BY 절이 있을 수 있습니다 .이 절은 number로 출력 열을 참조 해야 합니다. ORDER BY 절이 포함 되어 있으면 전체 결과에 영향을 줍니다.  
  
 UNION 절을 사용 하 여 외부 조인을 시뮬레이션할 수도 있습니다.  
  
 쿼리에서 두 테이블을 조인 하는 경우 조인 필드에 일치 하는 값을 가진 레코드만 출력에 포함 됩니다. 부모 테이블의 레코드에 자식 테이블의 해당 레코드가 없는 경우 부모 테이블의 레코드는 출력에 포함 되지 않습니다. 외부 조인을 사용 하면 부모 테이블의 모든 레코드를 자식 테이블의 일치 레코드와 함께 출력에 포함할 수 있습니다. Visual FoxPro에서 외부 조인을 만들려면 다음 예제와 같이 중첩 된 SELECT 명령을 사용 해야 합니다.  
  
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
>  각 세미콜론 바로 앞에 공백을 포함 하는지 확인 합니다. 그렇지 않으면 오류가 표시 됩니다.  
  
 UNION 절 앞의 명령 섹션에서는 일치 하는 값이 있는 두 테이블의 레코드를 선택 합니다. 관련 송장이 없는 고객 회사는 포함 되지 않습니다. UNION 절 다음의 명령 섹션에서는 orders 테이블에 일치 하는 레코드가 없는 customer 테이블의 레코드를 선택 합니다.  
  
 명령의 두 번째 섹션과 관련 하 여 다음 사항에 유의 하십시오.  
  
-   괄호 안의 SELECT 문이 먼저 처리 됩니다. 이 문은 orders 테이블에서 모든 고객 번호의 선택 항목을 만듭니다.  
  
-   WHERE 절은 customer 테이블에서 orders 테이블에 없는 모든 고객 번호를 찾습니다. 명령의 첫 번째 섹션은 orders 테이블에 고객 번호가 있는 모든 회사를 제공 했으므로 이제 customer 테이블의 모든 회사가 쿼리 결과에 포함 됩니다.  
  
-   공용 구조체에 포함 된 테이블의 구조는 동일 해야 하므로 두 번째 SELECT 문에는 두 개의 자리 표시 자가 있어야 합니다. 첫 번째 select 문에서는 *order_id* 및 *orders. emp_id* 를 표시 합니다.  
  
    > [!NOTE]  
    >  자리 표시자는 표시 되는 필드와 동일한 형식 이어야 합니다. 필드가 날짜 형식이 면 자리 표시 자가 {//} 여야 합니다. 필드가 문자 필드인 경우 자리 표시자는 빈 문자열 ("") 이어야 합니다.  
  
 ORDER BY *Order_Item* [ASC &#124; desc] [, *Order_Item* [asc &#124; desc] ...]  
 하나 이상의 열에 있는 데이터를 기반으로 쿼리 결과를 정렬 합니다. 각 *Order_Item* 는 쿼리 결과의 열과 일치 해야 하며 다음 중 하나일 수 있습니다.  
  
-   기본 SELECT 절에서 하위 쿼리가 아닌 select 항목인 FROM 테이블의 필드 이기도 합니다.  
  
-   결과 테이블에서 열의 위치를 나타내는 숫자 식입니다. 맨 왼쪽 열은 숫자 1입니다.  
  
 ASC는 주문 항목이 나 항목에 따라 쿼리 결과의 오름차순을 지정 하 고 ORDER BY에 대 한 기본값입니다.  
  
 DESC는 쿼리 결과의 내림차순을 지정 합니다.  
  
 ORDER BY를 사용 하 여 순서를 지정 하지 않으면 쿼리 결과가 정렬 되지 않은 것으로 나타납니다.  
  
## <a name="remarks"></a>설명  
 SELECT는 다른 Visual FoxPro 명령과 마찬가지로 Visual FoxPro에 기본 제공 되는 SQL 명령입니다. SELECT를 사용 하 여 쿼리를 발생 시킬 때 Visual FoxPro는 쿼리를 해석 하 고 테이블에서 지정 된 데이터를 검색 합니다. 명령 프롬프트 창이 나 Visual FoxPro 프로그램 (다른 Visual FoxPro 명령과 마찬가지로)에서 SELECT 쿼리를 만들 수 있습니다.  
  
> [!NOTE]  
>  SET FILTER에 지정 된 현재 필터 조건을 준수 하지 않습니다를 선택 합니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문 SELECT를 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 명령이 ODBC 이스케이프 시퀀스를 포함 하지 않는 한 변환 하지 않고 명령을 Visual FoxPro SELECT 명령으로 변환 합니다. ODBC 이스케이프 시퀀스로 묶인 항목은 Visual FoxPro 구문으로 변환 됩니다. ODBC 이스케이프 시퀀스를 사용 하는 방법에 대 한 자세한 내용은 [시간 및 날짜 함수](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) 및 *Microsoft odbc 프로그래머 참조*에서 [odbc의 이스케이프 시퀀스](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [삽입-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md)   
 [정확한 설정](../../odbc/microsoft/set-exact-command.md)
