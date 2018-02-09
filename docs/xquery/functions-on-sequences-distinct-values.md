---
title: "distinct-values 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4355506371dfbb5db0b6baea519d96ea5ddab6a9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-sequences---distinct-values"></a>시퀀스-고유 값 함수
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  값에 지정 된 시퀀스에서 중복 제거 *$arg*합니다. 경우 *$arg* 이 빈 시퀀스인 경우 함수는 빈 시퀀스를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 원자 값의 시퀀스입니다.  
  
## <a name="remarks"></a>주의  
 모든 유형의 원자화 된 값으로 전달 되는 **distinct-values ()** 동일 기준 유형의 하위 유형 이어야 합니다. 허용 되는 기본 형식을 지 원하는 형식이 되는 **eq** 작업 합니다. 이러한 유형에는 3가지 기본 제공 숫자 기본 유형, 날짜/시간 기본 유형, xs:string, xs:boolean 및 xdt:untypedAtomic이 포함됩니다. xdt:untypedAtomic 유형의 값은 xs:string으로 캐스팅됩니다. 이러한 유형이 혼합되어 있거나 다른 유형의 다른 값이 전달되면 정적 오류가 발생합니다.  
  
 결과 **distinct-values ()** xdt: untypedatomic의 경우 xs: string 같이 전달 된 유형의 기본 유형을 원래 카디널리티와 함께 수신 합니다. 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 발생합니다.  
  
 xs:string 유형의 값은 XQuery 기본 Unicode Codepoint Collation과 비교됩니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>1. distinct-values() 함수를 사용하여 시퀀스에서 중복 값 제거  
 이 예제에서는 전화 번호를 포함 하는 XML 인스턴스에 할당 됩니다는 **xml** 유형 변수입니다. 이 변수 사용 하 여 지정 된 XQuery에서 **distinct-values ()** 함수의 중복 항목을 포함 하지 않는 전화 번호 목록을 컴파일합니다.  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 다음은 결과입니다.  
  
```  
111-111-1111 222-222-2222    
```  
  
 다음 쿼리에서 숫자 (1, 1, 2) 시퀀스 전달는 **distinct-values ()** 함수입니다. 그러면 함수는 해당 시퀀스에서 중복을 제거하고 다른 두 값을 반환합니다.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 쿼리는 1, 2를 반환합니다.  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **distinct-values ()** 함수 정수 값을 xs: decimal에 매핑합니다.  
  
-   **distinct-values ()** 함수 앞에서 언급 한 형식 및 지원 기본 종류의 혼합을 지원 하지 않습니다.  
  
-   **distinct-values ()** xs: duration 값에는 함수가 지원 되지 않습니다.  
  
-   데이터 정렬을 제공하는 구문 옵션은 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
