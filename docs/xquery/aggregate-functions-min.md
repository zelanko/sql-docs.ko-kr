---
title: "min 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7227bd87057f6cce28d2c63bfe514e3912bf628c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="aggregate-functions---min"></a>집계 함수-분
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  원자 값의 시퀀스에서 반환 *$arg*, 하나의 항목 값을 사용 하면 다른 모든 보다 작습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 최소값을 반환할 항목의 시퀀스입니다.  
  
## <a name="remarks"></a>주의  
 모든 유형의 원자화 된 값으로 전달 되는 **min ()** 동일 기준 유형의 하위 유형 이어야 합니다. 허용 되는 기본 형식을 지 원하는 형식이 되는 **gt** 작업 합니다. 이러한 유형에는 3가지 기본 제공 숫자 기본 유형, 날짜/시간 기본 유형, xs:string, xs:boolean 및 xdt:untypedAtomic이 포함됩니다. xdt:untypedAtomic 유형의 값이 xs:double로 캐스팅됩니다. 이러한 종류의 혼합이 또는 다른 형식의 다른 값을 전달 되는 경우 정적 오류가 발생 합니다.  
  
 결과 **min ()** xdt: untypedatomic의 경우 xs: double 처럼 전달 유형의 기본 유형을 수신 합니다. 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 반환됩니다.  
  
 **min ()** 함수 입력된 시퀀스에서 다른 보다 작은 시퀀스의 값 중 하나를 반환 합니다. xs:string 값의 경우 기본 Unicode Codepoint Collation이 사용됩니다. 입력된 시퀀스에서 값이 무시 되는 xdt: untypedatomic 값을 xs: double로 캐스팅할 수 없는, 경우 *$arg*합니다. 입력이 동적으로 계산된 빈 시퀀스이면 빈 시퀀스가 반환됩니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>1. min() XQuery 함수를 사용하여 노동 시간이 최소인 업무 센터 위치 찾기  
 다음 쿼리는 제품 모델(ProductModelID=7)의 제조 프로세스에서 노동 시간이 최소인 모든 업무 센터 위치를 검색합니다. 일반적으로 다음과 같이 한 위치가 반환됩니다. 여러 위치에서 최소 노동 시간이 같은 경우 해당 위치가 모두 반환됩니다.  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
-   **네임 스페이스** 키워드 XQuery 프롤로그에 네임 스페이스 접두사를 정의 합니다. 그러면 이 접두사는 XQuery 본문에 사용됩니다.  
  
 XQuery 본문에는 XML을 생성 한 \<위치 >은 WCID 요소 및 **LaborHrs** 특성입니다.  
  
-   또한 이 쿼리는 ProductModelID 및 이름 값을 검색합니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **min ()** 함수는 모든 정수를 xs: decimal에 매핑합니다.  
  
-   **min ()** xs: duration 유형의 값에는 함수가 지원 되지 않습니다.  
  
-   여러 기본 유형 범위의 유형이 혼합된 시퀀스는 지원되지 않습니다.  
  
-   데이터 정렬을 제공하는 구문 옵션은 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
