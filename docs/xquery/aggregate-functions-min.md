---
title: min 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
author: rothja
ms.author: jroth
ms.openlocfilehash: 29e5718debadb4725bc9d9ebcd499c261ed23d54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985755"
---
# <a name="aggregate-functions---min"></a>집계 함수 - min
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  원자 값의 시퀀스에서 반환 *$arg*, 값이 다른 항목 보다 작은 항목 하나를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 최소값을 반환할 항목의 시퀀스입니다.  
  
## <a name="remarks"></a>설명  
 **Min ()** 에 전달 되는 원자화 된 값의 모든 형식은 동일한 기본 형식의 하위 형식 이어야 합니다. 허용 되는 기본 형식은 **gt** 작업을 지 원하는 형식입니다. 이러한 유형에는 3가지 기본 제공 숫자 기본 유형, 날짜/시간 기본 유형, xs:string, xs:boolean 및 xdt:untypedAtomic이 포함됩니다. xdt:untypedAtomic 유형의 값이 xs:double로 캐스팅됩니다. 이러한 형식이 혼합 되어 있거나 다른 형식의 다른 값이 전달 되 면 정적 오류가 발생 합니다.  
  
 **Min ()** 의 결과는 Xdt: untypedAtomic의 경우 xs: double과 같이 전달 된 유형의 기본 유형을 수신 합니다. 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 반환됩니다.  
  
 **Min ()** 함수는 시퀀스에서 입력 시퀀스의 다른 값 보다 작은 값 하나를 반환 합니다. xs:string 값의 경우 기본 Unicode Codepoint Collation이 사용됩니다. Xdt: untypedAtomic 값을 xs: double로 캐스팅할 수 없는 경우 값은 *$arg*입력 시퀀스에서 무시 됩니다. 입력이 동적으로 계산된 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. min() XQuery 함수를 사용하여 노동 시간이 최소인 업무 센터 위치 찾기  
 다음 쿼리는 제품 모델(ProductModelID=7)의 제조 프로세스에서 노동 시간이 최소인 모든 업무 센터 위치를 검색합니다. 일반적으로 다음과 같이 한 위치가 반환됩니다. 여러 위치에서 최소 노동 시간이 같은 경우 해당 위치가 모두 반환됩니다.  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   XQuery 프롤로그의 **namespace** 키워드는 네임 스페이스 접두사를 정의 합니다. 그러면 이 접두사는 XQuery 본문에 사용됩니다.  
  
 XQuery 본문은 WCID 및 **LaborHrs** 특성을 사용 \<하 여 위치> 요소가 있는 XML을 생성 합니다.  
  
-   또한 이 쿼리는 ProductModelID 및 이름 값을 검색합니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **Min ()** 함수는 모든 정수를 xs: decimal로 매핑합니다.  
  
-   Xs: duration 형식의 값에 대 한 **min ()** 함수는 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
-   데이터 정렬을 제공하는 구문 옵션은 지원되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
