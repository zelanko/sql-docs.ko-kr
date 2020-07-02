---
title: XPath 데이터 형식 (SQLXML)
description: SQLXML 4.0의 XPath 데이터 형식 및 Microsoft SQL Server 및 XSD (XML 스키마) 데이터 형식과 비교 하는 방법에 대해 알아봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eade5e3328993176f8795d27e511902a42468192
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764871"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 데이터 형식(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath 및 XSD (XML 스키마)는 데이터 형식이 매우 다릅니다. 예를 들어 XPath에는 정수나 날짜 데이터 형식이 없지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 XSD에는 이러한 데이터 형식이 많습니다. XSD는 시간 값에 나노초 정밀도를 사용하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 최대 1/300초의 정밀도를 사용합니다. 따라서 한 데이터 형식을 다른 데이터 형식에 매핑할 수 없는 경우도 있습니다. 데이터 형식을 XSD 데이터 형식에 매핑하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [데이터 형식 강제 변환 및 sql: datatype 주석 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)을 참조 하세요.  
  
 XPath에는 **문자열**, **숫자**및 **부울**의 세 가지 데이터 형식이 있습니다. **Number** 데이터 형식은 항상 IEEE 754 배정밀도 부동 소수점입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float (53)** 데이터 형식은 XPath **번호**와 가장 비슷합니다. 그러나 **float (53)** 는 정확히 IEEE 754이 아닙니다. 예를 들어 NaN(Not-a-Number)과 무한대는 모두 사용되지 않습니다. 숫자가 아닌 문자열을 **숫자로** 변환 하려고 시도 하 고 0으로 나누려고 하면 오류가 발생 합니다.  
  
## <a name="xpath-conversions"></a>XPath 변환  
 `OrderDetail[@UnitPrice > "10.0"]` 같은 XPath 쿼리를 사용할 경우 암시적/명시적 데이터 형식 변환으로 인해 쿼리의 의미가 미세하게 변경될 수 있습니다. 따라서 XPath 데이터 형식의 구현 방법을 올바르게 이해하고 있어야 합니다. XPath 언어 사양, XPath (XML Path Language) 버전 1.0 W3C 제안 권장 사항 8 월 1999은의 W3C 웹 사이트에서 찾을 수 있습니다 http://www.w3.org/TR/1999/PR-xpath-19991008.html .  
  
 XPath 연산자는 다음의 네 범주로 나뉩니다.  
  
-   부울 연산자(and, or)  
  
-   관계형 연산자 ( \<, > , \<=, > =)  
  
-   같음 연산자(=, !=)  
  
-   산술 연산자(+, -, *, div, mod)  
  
 연산자 범주마다 해당 피연산자를 변환하는 방법이 다릅니다. XPath 연산자는 필요한 경우 피연산자를 암시적으로 변환합니다. 산술 연산자는 피연산자를 **숫자로**변환 하 고 숫자 값을 반환 합니다. 부울 연산자는 피연산자를 **부울**로 변환 하 고 부울 값을 반환 합니다. 관계형 연산자와 같음 연산자는 부울 값을 반환합니다. 그러나 다음 표에서 볼 수 있듯이 피연산자의 원래 데이터 형식에 따라 서로 다른 변환 규칙이 적용됩니다.  
  
|피연산자|관계형 연산자|같음 연산자|  
|-------------|-------------------------|-----------------------|  
|두 피연산자가 모두 노드 집합입니다.|한 집합에 노드가 있는 경우에만 TRUE이 고 두 번째 집합에는 해당 **문자열** 값의 비교가 true 인 노드가 있는 경우에만 true입니다.|같습니다.|  
|하나는 노드 집합이 고 다른 하나는 **문자열**입니다.|**숫자로**변환할 때와 같이 노드 집합에 노드가 있는 경우에만 true이 고 **number** 로 변환 된 **문자열과** 비교 하는 경우 true입니다.|**문자열로**변환할 때와 같이 노드 집합에 노드가 있는 경우에만 true이 고, 그렇지 않으면 **문자열과** 비교 합니다.|  
|하나는 노드 집합이 고 다른 하나는 **숫자**입니다.|**숫자로**변환할 때와 같이 노드 집합에 노드가 있는 경우에만 **true이 고, 숫자와** 의 비교는 true입니다.|같습니다.|  
|하나는 노드 집합이 고 다른 하나는 **부울**입니다.|**부울** 로 변환 된 다음 **숫자로**변환 되는 경우와 같이 노드 집합에 노드가 있는 **경우에만** true **로 변환 됩니다** .|**부울**로 변환할 때 노드 집합에 노드가 있는 경우에만 **true이 고, 부울과** 비교 하면 true입니다.|  
|둘 모두 노드 집합이 아닙니다.|두 피연산자를 **숫자로** 변환한 다음 비교 합니다.|두 피연산자를 모두 일반 형식으로 변환한 다음 비교합니다. 부울 인 경우 **부울** 로 변환 하 **고, 숫자**이면 **number** 로 변환 **합니다.** 그렇지 않으면 **문자열로**변환 합니다.|  
  
> [!NOTE]  
>  XPath 관계형 연산자는 항상 피연산자를 **숫자로**변환 하므로 **문자열** 을 비교할 수 없습니다. 날짜 비교를 포함 하기 위해 SQL Server 2000는 XPath 사양에 대 한 이러한 변형을 제공 합니다. 관계 연산자 **가 문자열** 을 **문자열과**비교 하거나, 노드 집합 **을 문자열 또는**문자열 값 노드 집합으로 설정 하는 경우 문자열 비교 ( **숫자** 비교가 아님 **)가 수행** 됩니다.  
  
## <a name="node-set-conversions"></a>노드 집합 변환  
 노드 집합 변환이 항상 직관적이지는 않습니다. 노드 집합은 집합에서 첫 번째 노드의 문자열 값을 가져와 **문자열로** 변환 됩니다. 노드 집합을 **문자열로**변환 하 고 **문자열** 을 **숫자로**변환 하 여 **숫자로** 변환 합니다. 노드 집합은 존재 여부를 테스트 하 여 **부울** 로 변환 됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 노드 집합에 대해 위치 선택을 수행하지 않습니다. 예를 들어 XPath 쿼리 `Customer[3]`는 세 번째 고객을 의미하는데 이러한 종류의 위치 선택이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 지원되지 않습니다. 따라서 XPath 사양에서 설명 하는 노드 집합-**문자열** 또는 노드 집합-**숫자** 변환이 구현 되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 XPath 사양에 "첫 번째" 의미 체계가 지정된 경우 항상 "임의" 의미 체계를 사용합니다. 예를 들어 W3C XPath 사양을 기반으로 하는 XPath 쿼리는 `Order[OrderDetail/@UnitPrice > 10.0]` **단가** 가 10.0 보다 큰 첫 번째 **orderdetail** 이 포함 된 주문을 선택 합니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 XPath 쿼리는 **단가** 가 10.0 보다 큰 **orderdetail** 이 포함 된 주문을 선택 합니다.  
  
 **부울** 로 변환 하면 존재 테스트가 생성 됩니다. 따라서 XPath 쿼리는 `Products[@Discontinued=true()]` sql 식 "products. 단종 = 1"이 아니라 sql 식 "products. 단종 함은 null이 아닙니다."와 동일 합니다. 쿼리를 후자의 SQL 식과 동일 하 게 만들려면 먼저 노드 집합을 **숫자**와 같은**부울** 이 아닌 형식으로 변환 합니다. 예: `Products[number(@Discontinued) = true()]`  
  
 대부분의 연산자는 노드 집합의 임의 노드 또는 특정 노드에 대해 TRUE이면 TRUE가 되도록 정의되어 있으므로 노드 집합이 비어 있으면 이러한 연산의 결과가 항상 FALSE입니다. 따라서 A가 비어 있으면 `A = B`와 `A != B`는 모두 FALSE이고 `not(A=B)`와 `not(A!=B)`는 TRUE입니다.  
  
 일반적으로 열에 매핑되는 특성이 나 요소는 데이터베이스의 해당 열 값이 **null**이 아닌 경우에 존재 합니다. 행에 매핑되는 요소는 행의 자식이 있는 경우에만 존재합니다.  
  
> [!NOTE]  
>  로 주석이 지정 된 요소 **는** 항상 존재 합니다. 따라서 **is 상수** 요소에는 XPath 조건자를 사용할 수 없습니다.  
  
 노드 집합이 **문자열** 또는 **숫자로**변환 되는 경우 주석이 추가 된 스키마에서 해당 XDR 형식 (있는 경우)을 검사 하 고 해당 형식을 사용 하 여 필요한 변환을 결정 합니다.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>XDR 데이터 형식을 XPath 데이터 형식에 매핑  
 다음 표에서와 같이 노드의 XPath 데이터 형식은 스키마의 XDR 데이터 형식에서 파생 됩니다. 노드 **EmployeeID** 는 설명 목적으로 사용 됩니다.  
  
|XDR 데이터 형식|해당<br /><br /> XPath 데이터 형식|사용되는 SQL Server 변환|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|해당 없음|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|문자열|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|해당 사항 없음(XPath에는 fixed14.4 XDR 데이터 형식에 해당하는 데이터 형식이 없음)|CONVERT(money, EmployeeID)|  
|date|문자열|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|문자열|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 날짜 및 시간 변환은 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 데이터 형식 또는 **문자열**을 사용 하 여 데이터베이스에 저장 되는지 여부에 맞게 설계 되었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime** 데이터 형식은 **timezone** 를 사용 하지 않으며 XML **time** 데이터 형식의 전체 자릿수 보다 작습니다. **Timezone** 데이터 형식이 나 추가 전체 자릿수를 포함 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **문자열** 형식을 사용 하 여에 데이터를 저장 합니다.  
  
 노드가 해당 XDR 데이터 형식에서 XPath 데이터 형식으로 변환될 때 한 XPath 데이터 형식에서 다른 XPath 데이터 형식으로의 추가 변환이 필요한 경우가 있습니다. 예를 들어 다음과 같은 XPath 쿼리를 살펴봅니다.  
  
```  
(@m + 3) = 4  
```  
  
 @m가 **고정 14.4** XDR 데이터 형식인 경우 XDR 데이터 형식에서 XPath 데이터 형식으로 변환 하는 작업은 다음을 사용 하 여 수행 됩니다.  
  
```  
CONVERT(money, m)  
```  
  
 이 변환에서는 노드가 `m` **고정 14.4** 에서 **money**로 변환 됩니다. 그러나 값 3을 추가하려면 추가 변환이 필요합니다.  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 이 XPath 식은 다음과 같이 계산됩니다.  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 다음 표에서 볼 수 있듯이 이 변환은 리터럴 또는 복합 식과 같은 다른 XPath 식에 적용되는 변환과 같습니다.  
  
||||||  
|-|-|-|-|-|  
||X는 알 수 없는 형식입니다.|X는 **문자열** 입니다.|X는 **숫자** 입니다.|X는 **부울** 입니다.|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN (X) > 0|X != 0|-|  
  
## <a name="examples"></a>예제  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. XPath 쿼리에서 데이터 형식 변환  
 주석이 추가 된 XSD 스키마에 대해 지정 된 다음 XPath 쿼리에서 쿼리는 **EmployeeID** 특성 값이 E-1 인 모든 **Employee** 노드를 선택 합니다. 여기서 "e-"는 **sql: id-접두사** 주석을 사용 하 여 지정 된 접두사입니다.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 쿼리의 조건자는 다음 SQL 식과 같습니다.  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 **Employeeid** 는 XSD 스키마에서 **id** (**idref**, **idrefs**, **nmtoken**, **nmtokens**등)의 데이터 형식 값 중 하나 이므로 **employeeid** 는 앞에서 설명한 변환 규칙을 사용 하 여 **문자열** XPath 데이터 형식으로 변환 됩니다.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 "E-" 접두사가 문자열에 추가된 다음 그 결과가 `N'E-1'`과 비교됩니다.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. XPath 쿼리에서 몇 가지 데이터 형식 변환 수행  
 주석이 추가된 XSD 스키마에 대해 지정된 XPath 쿼리 `OrderDetail[@UnitPrice * @OrderQty > 98]`을 살펴봅니다.  
  
 이 XPath 쿼리는 조건자를 충족 하는 모든 요소를 반환 합니다 **\<OrderDetail>** `@UnitPrice * @OrderQty > 98` . 주석이 추가 된 스키마에서 **UnitPrice** 에 **고정 14.4** 데이터 형식이 주석으로 추가 되는 경우이 조건자는 SQL 식과 같습니다.  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 XPath 쿼리에서 값 변환 시 첫 번째 변환에서는 XDR 데이터 형식을 XPath 데이터 형식으로 변환합니다. 위의 표에 설명 된 대로 **UnitPrice** 의 XSD 데이터 형식이 **고정 14.4**이므로이는 첫 번째 변환입니다.  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 산술 연산자는 피연산자를 **숫자** XPath 데이터 형식으로 변환 하기 때문에 값이 **float (53)** 로 변환 되는 두 번째 변환 (한 xpath 데이터 형식에서 다른 xpath 데이터 형식으로)이 적용 됩니다 (**Float (53)** 은 xpath **number** 데이터 형식에 가깝습니다).  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 **Orderqty** 특성에 XSD 데이터 형식이 없으면 **orderqty** 는 단일 변환에서 **숫자** XPath 데이터 형식으로 변환 됩니다.  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 마찬가지로 값 98은 **숫자** XPath 데이터 형식으로 변환 됩니다.  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  스키마에 사용된 XSD 데이터 형식이 데이터베이스의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 호환되지 않거나 허용되지 않는 XPath 데이터 형식 변환이 수행되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환할 수 있습니다. 예를 들어 **employeeid** 특성에 **id 접두사** 주석을 추가 하는 경우 `Employee[@EmployeeID=1]` **employeeid** 는 **id 접두사** 주석을 포함 하 고 **숫자로**변환할 수 없으므로 XPath에서 오류를 생성 합니다.  
  
  
