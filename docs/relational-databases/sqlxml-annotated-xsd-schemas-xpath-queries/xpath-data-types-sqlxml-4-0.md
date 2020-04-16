---
title: XPath 데이터 유형(SQLXML)
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
ms.openlocfilehash: 089b2b006d0159c63e480c8627762ac37dec98b8
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "75247087"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 데이터 형식(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath 및 XML 스키마(XSD)는 매우 다른 데이터 형식을 가지고 있습니다. 예를 들어 XPath에는 정수나 날짜 데이터 형식이 없지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 XSD에는 이러한 데이터 형식이 많습니다. XSD는 시간 값에 나노초 정밀도를 사용하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 최대 1/300초의 정밀도를 사용합니다. 따라서 한 데이터 형식을 다른 데이터 형식에 매핑할 수 없는 경우도 있습니다. 데이터 형식을 XSD 데이터 형식에 매핑하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자세한 내용은 데이터 형식 강제 변환 및 [SQLXML 4.0&#41;&#40;sql:datatype 어칭을 ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)참조하십시오.  
  
 XPath에는 **문자열,** **번호**및 **부울의**세 가지 데이터 형식이 있습니다. **숫자** 데이터 유형은 항상 IEEE 754 이중 정밀도 부동 소수점입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float(53)** 데이터 형식은 XPath **번호에**가장 가깝습니다. 그러나 **플로트(53)는** 정확히 IEEE 754가 아니다. 예를 들어 NaN(Not-a-Number)과 무한대는 모두 사용되지 않습니다. 숫자가 아닌 문자열을 **숫자로** 변환하고 0으로 나누려고 하면 오류가 발생합니다.  
  
## <a name="xpath-conversions"></a>XPath 변환  
 `OrderDetail[@UnitPrice > "10.0"]` 같은 XPath 쿼리를 사용할 경우 암시적/명시적 데이터 형식 변환으로 인해 쿼리의 의미가 미세하게 변경될 수 있습니다. 따라서 XPath 데이터 형식의 구현 방법을 올바르게 이해하고 있어야 합니다. XPath 언어 사양, XML 경로 언어 (XPath) 버전 1.0 W3C 제안 권장 사항 8 1999 년 http://www.w3.org/TR/1999/PR-xpath-19991008.html10 월 W3C 웹 사이트에서 찾을 수 있습니다.  
  
 XPath 연산자는 다음의 네 범주로 나뉩니다.  
  
-   부울 연산자(and, or)  
  
-   관계형 연산자 (,\<>, \<=, >=)  
  
-   같음 연산자(=, !=)  
  
-   산술 연산자(+, -, *, div, mod)  
  
 연산자 범주마다 해당 피연산자를 변환하는 방법이 다릅니다. XPath 연산자는 필요한 경우 피연산자를 암시적으로 변환합니다. 산술 연산자는 해당 산술을 **숫자로**변환하고 숫자 값을 생성합니다. 부울 연산자는 피연산을 **부울로**변환하고 부울 값을 생성합니다. 관계형 연산자와 같음 연산자는 부울 값을 반환합니다. 그러나 다음 표에서 볼 수 있듯이 피연산자의 원래 데이터 형식에 따라 서로 다른 변환 규칙이 적용됩니다.  
  
|피연산자|관계형 연산자|같음 연산자|  
|-------------|-------------------------|-----------------------|  
|두 피연산자가 모두 노드 집합입니다.|TRUE 경우 한 세트에 노드가 있고 두 번째 집합에 노드가 있는 경우에만 **문자열** 값의 비교가 TRUE입니다.|같습니다.|  
|하나는 노드 집합, 다른 하나는 **문자열입니다.**|TRUE 경우 노드 집합에 **노드가**있는 경우에만 숫자로 변환할 때 **숫자로** 변환된 **문자열과의** 비교가 TRUE입니다.|TRUE 경우 노드 집합에 **문자열로**변환할 때 **문자열과의** 비교가 TRUE인 경우에만 해당 노드가 있는 경우입니다.|  
|하나는 노드 집합, 다른 하나는 **숫자입니다.**|TRUE 경우 노드 집합에 **노드가**있는 경우에만 숫자로 변환할 때 **노드와 노드를** 비교하는 것이 TRUE입니다.|같습니다.|  
|하나는 노드 집합이고 다른 하나는 **부울입니다.**|TRUE 경우 노드 집합에 **부울로** 변환한 다음 **번호로**변환할 때 **숫자로** 변환된 **부울과** 의 비교가 TRUE입니다.|TRUE 경우 노드 집합에 **부울로**변환할 때 **부울과의** 비교가 TRUE인 경우에만 노드가 있는 경우입니다.|  
|둘 모두 노드 집합이 아닙니다.|두 개의 나연을 **숫자로** 변환한 다음 비교합니다.|두 피연산자를 모두 일반 형식으로 변환한 다음 비교합니다. **부울인** 경우 **부울로**변환, **숫자** 중 하나가 **숫자인**경우; 그렇지 않으면 **문자열로**변환합니다.|  
  
> [!NOTE]  
>  XPath 관계형 연산자는 항상 해당 카페랜드를 **숫자로**변환하므로 **문자열** 비교는 불가능합니다. 날짜 비교를 포함하기 위해 SQL Server 2000은 XPath 사양에 대한 이러한 변형을 제공합니다: 관계형 연산자가 **문자열과 문자열을** 비교하는 **경우,** 노드 집합을 **문자열로**설정하거나 문자열 값 노드 집합을 문자열 값 노드 집합으로 설정하면 **문자열** **비교(숫자** 비교가 아님)가 수행됩니다.  
  
## <a name="node-set-conversions"></a>노드 집합 변환  
 노드 집합 변환이 항상 직관적이지는 않습니다. 노드 집합은 집합의 첫 번째 노드의 문자열 값만 사용하여 **문자열로** 변환됩니다. 노드 집합은 **문자열을 문자열로**변환한 다음 문자열을 **번호로** **변환하여** **숫자로** 변환됩니다. 노드 집합은 노드 집합의 존재를 테스트하여 **부울로** 변환됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 노드 집합에 대해 위치 선택을 수행하지 않습니다. 예를 들어 XPath 쿼리 `Customer[3]`는 세 번째 고객을 의미하는데 이러한 종류의 위치 선택이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 지원되지 않습니다. 따라서 XPath 사양에 설명된 대로**노드-문자열** 또는 노드 집합-수**변환구현** 되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 XPath 사양에 "첫 번째" 의미 체계가 지정된 경우 항상 "임의" 의미 체계를 사용합니다. 예를 들어 W3C XPath 사양에 따라 XPath 쿼리는 `Order[OrderDetail/@UnitPrice > 10.0]` **UnitPrice가** 10.0보다 큰 첫 번째 **OrderDetail을** 사용하여 해당 주문을 선택합니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 XPath 쿼리는 **UnitPrice가** 10.0보다 큰 **OrderDetail을** 사용하여 해당 주문을 선택합니다.  
  
 **부울로** 변환하여 존재 테스트를 생성합니다. 따라서 XPath 쿼리는 `Products[@Discontinued=true()]` SQL 식 "Products.단종은 null이 아닙니다"와 동일하며 SQL 식 "Products.단종 = 1"이 아닙니다. 쿼리를 후자의 SQL 식과 동일하게 만들려면 먼저 노드 집합을 **숫자와**같은**부울** 형식이 아닌 유형으로 변환합니다. `Products[number(@Discontinued) = true()]`)을 입력합니다.  
  
 대부분의 연산자는 노드 집합의 임의 노드 또는 특정 노드에 대해 TRUE이면 TRUE가 되도록 정의되어 있으므로 노드 집합이 비어 있으면 이러한 연산의 결과가 항상 FALSE입니다. 따라서 A가 비어 있으면 `A = B`와 `A != B`는 모두 FALSE이고 `not(A=B)`와 `not(A!=B)`는 TRUE입니다.  
  
 일반적으로 데이터베이스에 있는 해당 열의 값이 **null이**아닌 경우 열에 매핑되는 특성 또는 요소가 존재합니다. 행에 매핑되는 요소는 행의 자식이 있는 경우에만 존재합니다.  
  
> [!NOTE]  
>  **상수로** 추가된 요소는 항상 존재합니다. 따라서 XPath 조건자 에서는 **상수** 요소에 사용할 수 없습니다.  
  
 노드 집합이 **문자열** 또는 **번호로**변환되면 해당 XDR 형식(있는 경우)이 추가된 스키마에서 검사되고 해당 형식이 필요한 변환을 결정하는 데 사용됩니다.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>XDR 데이터 형식을 XPath 데이터 형식에 매핑  
 노드의 XPath 데이터 형식은 다음 표에 표시된 스키마의 XDR 데이터 형식에서 **파생됩니다(사용자** ID 노드는 설명 목적으로 사용됨).  
  
|XDR 데이터 형식|해당<br /><br /> XPath 데이터 형식|사용되는 SQL Server 변환|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|해당 없음|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|문자열|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|해당 사항 없음(XPath에는 fixed14.4 XDR 데이터 형식에 해당하는 데이터 형식이 없음)|CONVERT(money, EmployeeID)|  
|date|문자열|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|문자열|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 날짜 및 시간 변환은 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 데이터 형식 또는 **문자열을**사용하여 데이터베이스에 저장되는지 여부를 작동하도록 설계되었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 데이터 형식은 표준 **시간대를** 사용하지 않으며 XML **시간** 데이터 형식보다 정밀도가 낮습니다. **시간대** 데이터 형식 또는 추가 정밀도를 포함하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **문자열** 형식을 사용하여 데이터를 저장합니다.  
  
 노드가 해당 XDR 데이터 형식에서 XPath 데이터 형식으로 변환될 때 한 XPath 데이터 형식에서 다른 XPath 데이터 형식으로의 추가 변환이 필요한 경우가 있습니다. 예를 들어 다음과 같은 XPath 쿼리를 살펴봅니다.  
  
```  
(@m + 3) = 4  
```  
  
 @m **fixed14.4** XDR 데이터 형식인 경우 다음을 사용하여 XDR 데이터 형식에서 XPath 데이터 유형으로 변환이 수행됩니다.  
  
```  
CONVERT(money, m)  
```  
  
 이 변환에서 노드는 `m` **fixed14.4에서** **돈으로**변환됩니다. 그러나 값 3을 추가하려면 추가 변환이 필요합니다.  
  
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
||X는 알 수 없는 형식입니다.|X는 **문자열입니다.**|X는 **숫자입니다.**|X는 **부울**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>예  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. XPath 쿼리에서 데이터 형식 변환  
 추가된 XSD 스키마에 대해 지정된 다음 XPath 쿼리에서 쿼리는 **Sql:id 접두사** 어구를 사용하여 지정된 접두사인 E-1의 **EmployeeID** 특성 값을 가진 모든 **Employee** 노드를 선택합니다.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 쿼리의 조건자는 다음 SQL 식과 같습니다.  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 **EmployeeID는** XSD 스키마의**id(idref,** **idrefs,** **nmtoken,** **nmtokens**등) 데이터 형식 값 중 하나이므로 **EmployeeID는** 앞에서 설명한 변환 규칙을 사용하여 **문자열** XPath 데이터 유형으로 변환됩니다. **id**  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 "E-" 접두사가 문자열에 추가된 다음 그 결과가 `N'E-1'`과 비교됩니다.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. XPath 쿼리에서 몇 가지 데이터 형식 변환 수행  
 주석이 추가된 XSD 스키마에 대해 지정된 XPath 쿼리 `OrderDetail[@UnitPrice * @OrderQty > 98]`을 살펴봅니다.  
  
 이 XPath 쿼리는 조건어를 `@UnitPrice * @OrderQty > 98` ** \<** 충족하는 모든 OrderDetail>요소를 반환합니다. **UnitPrice에** 추가된 스키마에 **fixed14.4** 데이터 형식이 있는 경우 이 술어는 SQL 식과 같습니다.  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 XPath 쿼리에서 값 변환 시 첫 번째 변환에서는 XDR 데이터 형식을 XPath 데이터 형식으로 변환합니다. **UnitPrice의** XSD 데이터 형식은 이전 표에 설명된 대로 고정되어 있기 **때문에14.4,** 이것은 사용되는 첫 번째 변환입니다.  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 산술 연산자는 자신의 산술 연산자가 자신의 산연산을 XPath 데이터 **유형으로** 변환하기 때문에 값이 float(53)(float(53)에 가깝습니다.) 값이 **float(53)로** 변환되는 두 번째 변환(한 XPath 데이터 형식에서 다른 XPath 데이터 형식)이 적용됩니다.**float(53)** **number**  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 **OrderQty** 특성에 XSD 데이터 형식이 없다고 가정하면 **OrderQty는** 단일 변환에서 **숫자** XPath 데이터 유형으로 변환됩니다.  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 마찬가지로 값 98은 XPath 데이터 형식의 **숫자로** 변환됩니다.  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  스키마에 사용된 XSD 데이터 형식이 데이터베이스의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 호환되지 않거나 허용되지 않는 XPath 데이터 형식 변환이 수행되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환할 수 있습니다. 예를 들어 **EmployeeID** 특성에 **ID 접두사** 추가 가 추가된 경우 `Employee[@EmployeeID=1]` **EmployeeID에는** **ID 접두사** 부호가 있고 **번호로**변환할 수 없기 때문에 XPath는 오류를 생성합니다.  
  
  
