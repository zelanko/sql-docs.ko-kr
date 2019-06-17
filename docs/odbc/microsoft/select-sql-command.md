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
manager: craigg
ms.openlocfilehash: 0c2d991afa179fdfbb536853e302b33de8bf12e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127872"
---
# <a name="select---sql-command"></a>SELECT - SQL 명령
하나 이상의 테이블에서 데이터를 검색합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보를 참조 하세요 **드라이버 주의**합니다.  
  
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
>  A *하위*, 다음 인수에서 참조 하는 SELECT 내에서 선택 및 괄호로 묶어야 합니다. 동일한 수준에서 최대 2 개의 하위를 할 수 있습니다 (중첩 되지 않음) WHERE 절에 있습니다. (인수 섹션 참조). 하위 쿼리는 조인 조건이 여러 개 포함할 수 있습니다.  
  
 [ALL &#124; DISTINCT]   [*Alias*.] *Select_Item* [AS *Column_Name*]    [, [*Alias*.] *Select_Item* [AS *Column_Name*] ...]  
 SELECT 절에는 필드, 상수 및 쿼리 결과에 표시 되는 식을 지정 합니다.  
  
 기본적으로 쿼리 결과에 모든 행을 표시 모든 합니다.  
  
 DISTINCT는 쿼리 결과에서 중복 행을 제외합니다.  
  
> [!NOTE]  
>  SELECT 절 당 한 번만 DISTINCT를 사용할 수 있습니다.  
  
 *별칭*합니다. 일치 하는 항목 이름을 한정합니다. 각 항목을 사용 하 여 지정한 *Select_Item* 쿼리 결과의 열을 생성 합니다. 두 개 이상 항목 이름이 동일한 경우 테이블 별칭과 열이 중복 되지 않도록 하려면 항목 이름 앞에 마침표를 포함 합니다.  
  
 *Select_Item* 쿼리 결과에 포함할 항목을 지정 합니다. 항목에는 다음 중 하나일 수 있습니다.  
  
-   FROM 절의 테이블에서 필드의 이름입니다.  
  
-   동일한 상수 값이 쿼리 결과의 모든 행에 표시 됨을 지정 하는 상수입니다.  
  
-   사용자 정의 함수의 이름을 도움이 되는 식입니다.  
  
 **선택 된 사용자 정의 함수**  
  
 SELECT 절에서 사용자 정의 함수를 사용 하 여 확실 한 이점이 이지만 다음 제한 사항을 고려해 야 합니다.  
  
-   이러한 사용자 정의 함수 실행 되는 속도 선택으로 수행 된 작업의 속도 제한 될 수 있습니다. 사용자 정의 함수를 포함 하는 대규모 조작 API 및 C 또는 어셈블리 언어로 작성 된 사용자 정의 함수를 사용 하 여 더 잘 수행할 수 있습니다.  
  
-   선택에서 호출 하는 사용자 정의 함수에 값을 전달 하는 신뢰할 수 있는 유일한 방법은 호출 될 때 함수에 전달 된 인수 목록이 있습니다.  
  
-   실험을 FoxPro의 특정 버전에서 올바르게 작동 하는 화면이 금지 된 조작을 검색 하는 경우에 계속 이후 버전에서 작동 하지 않을 수도가 있습니다.  
  
 이러한 제한 사항 외에도 사용자 정의 함수는 SELECT 절에 허용 됩니다. 그러나 SELECT를 사용 하 여 성능이 저하 될 수 있습니다.  
  
 다음 필드 함수는 필드 또는 필드를 포함 하는 식을 선택 항목을 사용할 수 있습니다.  
  
-   AVG (*Select_Item*)-숫자 데이터 열의 평균을 계산 합니다.  
  
-   COUNT (*Select_Item*)-열에 선택 항목의 수를 계산 합니다. 그룹 쿼리 출력의 행 수를 셉니다.  
  
-   MIN (*Select_Item*)-의 가장 작은 값을 결정 *Select_Item* 열에서입니다.  
  
-   최대 (*Select_Item*)-의 가장 큰 값을 결정 *Select_Item* 열에서입니다.  
  
-   SUM (*Select_Item*)-숫자 데이터 열의 합계를 계산 합니다.  
  
 필드 함수를 중첩할 수 없습니다.  
  
 AS *Column_Name*  
 쿼리 출력에서 열 머리글을 지정합니다. 이 경우에 유용 *Select_Item* 식 또는 필드가 포함 함수 하려는 열에 의미 있는 이름을 지정 합니다. *Column_Name* 식일 수 있지만 테이블 필드 이름에 허용 되지 않는 문자 (예를 들어, 공백)를 포함할 수 없습니다.  
  
 FROM [*DatabaseName*!]*Table* [*Local_Alias*]   [, [*DatabaseName*!]*Table* [*Local_Alias*] ...]  
 쿼리를 검색 하는 데이터가 포함 된 테이블을 나열 합니다. 테이블이 없으면가 열려 있으면 Visual FoxPro 표시 합니다 **엽니다** 대화 상자의 파일 위치를 지정할 수 있도록 합니다. 이 열린 후에 쿼리가 완료 된 후 테이블 열린 상태로 유지 됩니다.  
  
 *DatabaseName*! 데이터 소스를 사용 하 여 지정 된 것과 다른 데이터베이스의 이름을 지정 합니다. 데이터 소스를 사용 하 여 데이터베이스를 지정 하지 않으면 테이블이 포함 된 데이터베이스의 이름을 포함 해야 합니다. 데이터베이스 이름 뒤에 오는 및 테이블 이름 앞에 느낌표 (!) 구분 기호를 포함 합니다.  
  
 *Local_Alias* 임시 테이블에서 명명 된 이름을 지정 합니다 *테이블*합니다. 로컬 별칭을 지정 하면 SELECT 문의 전체 테이블 이름 대신 로컬 별칭을 사용 해야 합니다. 로컬 별칭 Visual FoxPro 환경 영향을 주지 않습니다.  
  
 여기서 *JoinCondition* [AND *JoinCondition* ...]    [AND &#124; 또는 *FilterCondition* [AND &#124; 또는 *FilterCondition* ...]]  
 Visual FoxPro 쿼리 결과에서 특정 레코드만 포함 하도록 지시 합니다. 여러 테이블에서 데이터를 검색 하는 데 필요한 경우.  
  
 *JoinCondition* FROM 절에서 테이블을 연결 하는 필드를 지정 합니다. 쿼리에서 둘 이상의 테이블을 포함 하는 경우 첫 번째 후 모든 테이블에 대 한 조인 조건을 지정 해야 합니다.  
  
> [!IMPORTANT]  
>  조인 조건을 만들 때 다음 정보를 고려 합니다.  
  
-   쿼리에서 두 테이블을 포함 하 고 조인 조건을 지정 하지 않으면 첫 번째 테이블의 모든 레코드를 필터 조건으로 두 번째 테이블의 모든 레코드에 조인 됩니다. 이러한 쿼리는 길이가 긴 결과 생성할 수 있습니다.  
  
-   Visual FoxPro 빈 필드와 일치 하기 때문에 빈 필드를 사용 하 여 테이블을 조인 하는 경우에 주의 해야 합니다. 예를 들어 고객에 조인 합니다. ZIP 및 청구서를 보냅니다. 압축 및 쿼리 출력에 빈 필드에서 발생 하는 40,000 추가 레코드 100 빈 우편 번호를 포함 하는 고객 청구서 400 빈 우편 번호를 포함 하는 경우. 사용 된 **빈 ()** 쿼리 출력에서 빈 레코드를 제거 하는 함수입니다.  
  
-   AND 연산자를 사용 하 여 여러 개의 조인 조건이 연결 해야 합니다. 각 join 조건에는 다음 폼에 있습니다.  
  
     *FieldName1 비교 FieldName2*  
  
     *FieldName1* 한 테이블에서 필드의 이름은 *FieldName2* 은 다른 테이블에서 필드의 이름 및 *비교* 다음 표에 설명 된 연산자 중 하나입니다.  
  
|연산자|비교|  
|--------------|----------------|  
|=|같음|  
|==|정확 하 게 일치|  
|LIKE|SQL LIKE|  
|<>, !=, #|같지 않음|  
|>|두 개|  
|>=|보다 크거나 같음|  
|<|보다 작음|  
|<=|작거나 같음|  
  
 사용 하는 경우는 = 연산자, 문자열을 사용 하 여 역할 다르게 설정 ANSI 설정에 따라 합니다. ANSI 설정 OFF로 설정 되 면 Visual FoxPro Xbase 사용자에 게 익숙한 방식으로 문자열 비교를 처리 합니다. ANSI 설정 ON으로 설정 되 면 Visual FoxPro 문자열 비교에 대 한 ANSI 표준을 따릅니다. 참조 [ANSI 설정](../../odbc/microsoft/set-ansi-command.md) 하 고 [정확 하 게 설정](../../odbc/microsoft/set-exact-command.md) Visual FoxPro 문자열 비교를 수행 하는 방법에 대 한 자세한 내용은 합니다.  
  
 *FilterCondition* 레코드 쿼리 결과에 포함할 충족 해야 하는 조건을 지정 합니다. AND를 사용 하 여 연결을 원하는 개수 만큼 필터 쿼리에서 조건을 포함할 수 있습니다 또는 OR 연산자입니다. 논리 식의 값을 반전 하려면 NOT 연산자를 사용할 수도 있습니다 하거나 사용할 수 있습니다 **빈 ()** 빈 필드에 대 한 확인 합니다. *FilterCondition* 다음 예제에서 형식 중 하나를 수행할 수 있습니다.  
  
 **예제 1** *FieldName1 비교 FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **예제 2** *FieldName 비교 식*  
  
 `payments.amount >= 1000`  
  
 **예제 3** *FieldName 비교* 모든 (*하위*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 필터 조건 모두를 포함 하는 경우 필드에는 해당 레코드를 쿼리 결과에 포함할지 전에 하위 쿼리에 의해 생성 된 모든 값에 대 한 비교 조건을 충족 해야 합니다.  
  
 **예제 4** *FieldName 비교* ANY &#124; 일부 (*하위*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 필터 조건 또는 일부를 포함 하는 경우 필드에는 하나 이상의 하위 쿼리에 의해 생성 된 값에 대 한 비교 조건을 충족 해야 합니다.  
  
 다음 예제에서는 값의 지정된 된 범위 내의 필드의 값이 같은지를 확인 합니다.  
  
 **예제 5** *FieldName* [NOT] BETWEEN *Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 다음 예제에서는 하나 이상의 행에 하위 쿼리 조건을 충족 하는지 여부를 확인 합니다. 필터 조건이 True로 평가 되는 필터 조건을 EXISTS를 포함 하는 경우 (합니다. 하위 쿼리는 빈 집합을로 확인 되지 않으면 T.).  
  
 **예제 6** [NOT] EXISTS (*하위*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **예제 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 필터 조건에 포함 하는 경우 필드 전에 포함 해야 값 중 하나 쿼리 결과에 해당 레코드가 포함 됩니다.  
  
 **예제 8** *FieldName* [NOT] IN (*하위*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 다음 필드를 해당 레코드를 쿼리 결과에 포함할지 전에 하위 쿼리에서 반환한 값 중 하나를 포함 해야 합니다.  
  
 **예제 9** *FieldName* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 이 필터 조건과 일치 하는 각 필드에 대 한 검색 *cExpression*합니다. 백분율 기호 (%)을 사용할 수 있습니다. 및의 일부로 밑줄 (_) 와일드 카드 문자 *cExpression*합니다. 밑줄은 문자열에서 알 수 없는 단일 문자를 나타냅니다.  
  
 GROUP BY *GroupColumn* [합니다 *GroupColumn* ...]  
 하나 이상의 열 값에 따라 쿼리에서 행을 그룹화 합니다. *GroupColumn* 다음 중 하나일 수 있습니다.  
  
-   일반 테이블 필드의 이름입니다.  
  
-   SQL 필드 함수를 포함 하는 필드입니다.  
  
-   결과 테이블의 열 위치를 나타내는 숫자 식입니다. (맨 왼쪽 열 번호는 1입니다.)  
  
 필요 *FilterCondition*  
 쿼리 결과에 포함할 그룹 충족 해야 하는 필터 조건을 지정 합니다. HAVING 그룹화에 사용 해야 하 고 AND로 연결 원하는 개수 만큼 필터 조건을 포함할 수 있습니다 또는 OR 연산자입니다. 논리 식의 값을 반전 필요가 사용할 수 있습니다.  
  
 *FilterCondition* 하위 쿼리를 포함할 수 없습니다.  
  
 GROUP BY 절 없이 HAVING 절을 WHERE 절 처럼 동작합니다. HAVING 절에서 로컬 별칭과 필드 함수를 사용할 수 있습니다. HAVING 절에 없는 필드 함수를 포함 하는 경우 성능 향상을 위해 WHERE 절을 사용 합니다.  
  
 [[ALL] UNION *SELECTCommand*]  
 다른 선택의 최종 결과 하나의 선택의 최종 결과 결합합니다. 기본적으로 UNION 결합 된 결과 확인 하 고 중복 행을 제거 합니다. UNION 절이 여러 개를 결합 하려면 괄호를 사용 합니다.  
  
 공용 구조체를 방지 모든에서 결합된 된 결과에서 중복 행을 제거 합니다.  
  
 UNION 절 같은이 규칙을 따릅니다.  
  
-   하위 쿼리를 결합 하는 공용 구조체를 사용할 수 없습니다.  
  
-   SELECT 명령을 모두 쿼리 출력에 같은 수의 열을 있어야 합니다.  
  
-   다른 선택의 해당 열과 동일한 데이터 형식와 너비를 하나 선택의 쿼리 결과의 각 열 있어야 합니다.  
  
-   최종 SELECT만 출력 열 번호로 참조 해야 하는 ORDER BY 절을 가질 수 있습니다. ORDER BY 절을 포함 하는 경우 전체 결과를 영향을 줍니다.  
  
 또한 외부 조인을 시뮬레이션 하기 위해 UNION 절을 사용할 수 있습니다.  
  
 쿼리에서 두 테이블을 조인 하는 경우 조인 필드에서 일치 하는 값을 사용 하 여 레코드에만 출력에 포함 됩니다. 부모 테이블의 레코드에 해당 레코드가 없으면 자식 테이블의 부모 테이블에서 레코드를 출력에 포함 되지 않습니다. 외부 조인을 사용 하면 자식 테이블에서 일치 하는 레코드와 함께 출력에서 부모 테이블의 모든 레코드를 포함할 수 있습니다. Visual FoxPro를 외부 조인을 만들려면 다음 예제와 같이 중첩 된 SELECT 명령의 경우 사용 해야 합니다.  
  
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
>  바로 각 세미콜론 앞에 공간을 포함 해야 합니다. 그렇지 않으면 오류를 받게 됩니다.  
  
 UNION 절 모두 테이블에서 레코드를 선택 하기 전에 명령의 섹션은 일치 하는 값입니다. 연결 된 송장 없는 고객 회사 포함 되지 않습니다. UNION 절 다음에 명령 부분 일치 하는 orders 테이블의 레코드 없는 customer 테이블의 레코드를 선택 합니다.  
  
 명령의 두 번째 섹션에 관련 된 다음 note:  
  
-   SELECT 문은 괄호 안에 먼저 처리 됩니다. 이 문은 orders 테이블의 모든 고객 번호의 선택 영역을 만듭니다.  
  
-   WHERE 절 orders 테이블에 없는 customer 테이블의 모든 고객 번호를 찾습니다. 명령의 첫 번째 섹션 orders 테이블에서 고객 수 있었던 모든 회사를 제공 하기 때문에 customer 테이블의 모든 회사는 이제 쿼리 결과에 포함 됩니다.  
  
-   공용 구조체에 포함 된 테이블의 구조와 동일한 있어야 하므로 두 명의 자리 표시자를 나타내는 두 번째 SELECT 문은 *orders.order_id* 하 고 *orders.emp_id* 첫 번째 선택 문입니다.  
  
    > [!NOTE]  
    >  자리 표시자를 나타내는 필드와 동일한 형식 이어야 합니다. 필드가 날짜 형식인 경우에 자리 표시자 여야 합니다 {/ /}. 필드의 문자 필드 이면 자리 표시자는 빈 문자열일 ("").  
  
 ORDER BY *Order_Item* [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC] ...]  
 하나 이상의 열에 있는 데이터를 기반으로 쿼리 결과 정렬 합니다. 각 *Order_Item* 쿼리 결과에서 열과 일치 해야 하 고 다음 중 하나일 수 있습니다.  
  
-   (하위 쿼리)에 없는 기본 SELECT 절에서 선택 항목 이기도 FROM 테이블의 필드입니다.  
  
-   결과 테이블의 열 위치를 나타내는 숫자 식입니다. (맨 왼쪽 열은 1입니다.)  
  
 ASC 주문 항목 또는 항목에 따라 쿼리 결과 오름차순 순서를 지정 하 고 ORDER BY에 대 한 기본값입니다.  
  
 DESC는 쿼리 결과 대 한 내림차순을 지정합니다.  
  
 ORDER BY와 함께 순서를 지정 하지 않는 경우 쿼리 결과 순서가 지정 되지 않은 표시 됩니다.  
  
## <a name="remarks"></a>Remarks  
 선택은 다른 Visual FoxPro 명령 처럼 Visual FoxPro에 기본 제공 되는 SQL 명령입니다. 사용 하는 경우 쿼리를 제기 하기 위해 선택, Visual FoxPro 쿼리를 해석 하 고 테이블에서 지정된 된 데이터를 검색 합니다. (마찬가지로 다른 Visual FoxPro 명령) 명령 프롬프트 창 또는 Visual FoxPro 프로그램 내에서 SELECT 쿼리를 만들 수 있습니다.  
  
> [!NOTE]  
>  선택 설정 필터를 사용 하 여 지정 된 현재 필터 조건을 반영 되지 않습니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문을 선택 데이터 원본에 보내는 명령 ODBC 이스케이프 시퀀스가 포함 되어 있지 않으면 명령 Visual FoxPro ODBC 드라이버에 변환 하지 않아도 Visual FoxPro 선택 명령으로 변환 합니다. ODBC 이스케이프 시퀀스의 항목은 Visual FoxPro 구문으로 변환 됩니다. 이스케이프 시퀀스 ODBC를 사용 하는 방법에 대 한 자세한 내용은 [날짜 및 시간 함수](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) 및 합니다 *Microsoft ODBC 프로그래머 참조*를 참조 하세요 [ODBC의 이스케이프 시퀀스](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) .  
  
## <a name="see-also"></a>관련 항목  
 [CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [정확 하 게 설정](../../odbc/microsoft/set-exact-command.md)
