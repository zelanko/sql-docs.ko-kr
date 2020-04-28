---
title: 고유 값 함수 (XQuery) | Microsoft Docs
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
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
ms.openlocfilehash: d2f856c9b351c776651f08e66f90c7f567a5dcfc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68223730"
---
# <a name="functions-on-sequences---distinct-values"></a>시퀀스 함수 - distinct-values
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  *$Arg*에 지정 된 시퀀스에서 중복 값을 제거 합니다. *$Arg* 빈 시퀀스인 경우 함수는 빈 시퀀스를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 원자 값의 시퀀스입니다.  
  
## <a name="remarks"></a>설명  
 **고유 값 ()** 으로 전달 되는 원자화 된 값의 모든 형식은 동일한 기본 형식의 하위 형식 이어야 합니다. 허용 되는 기본 유형은 **eq** 작업을 지 원하는 형식입니다. 이러한 유형에는 3가지 기본 제공 숫자 기본 유형, 날짜/시간 기본 유형, xs:string, xs:boolean 및 xdt:untypedAtomic이 포함됩니다. xdt:untypedAtomic 유형의 값은 xs:string으로 캐스팅됩니다. 이러한 유형이 혼합되어 있거나 다른 유형의 다른 값이 전달되면 정적 오류가 발생합니다.  
  
 **고유 값 ()** 의 결과는 Xdt: untypedAtomic의 경우 xs: string과 같이 원래 카디널리티를 사용 하 여 전달 된 형식의 기본 형식을 받습니다. 입력이 정적으로 비어 있으면 비어 있다는 것이 유추되어 정적 오류가 발생합니다.  
  
 xs:string 유형의 값은 XQuery 기본 Unicode Codepoint Collation과 비교됩니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. distinct-values() 함수를 사용하여 시퀀스에서 중복 값 제거  
 이 예에서는 전화 번호를 포함 하는 XML 인스턴스가 **xml** 유형의 변수에 할당 됩니다. 이 변수에 대해 지정 된 XQuery는 **고유 값 ()** 함수를 사용 하 여 중복 항목이 없는 전화 번호 목록을 컴파일합니다.  
  
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
  
 다음 쿼리에서는 일련의 숫자 (1, 1, 2)가 **고유 값 ()** 함수에 전달 됩니다. 그러면 함수는 해당 시퀀스에서 중복을 제거하고 다른 두 값을 반환합니다.  
  
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
  
-   **고유 값 ()** 함수는 정수 값을 xs: decimal로 매핑합니다.  
  
-   **고유 값 ()** 함수는 앞에서 언급 한 형식만 지원 하며 기본 형식의 혼합은 지원 하지 않습니다.  
  
-   Xs: duration 값에 대 한 **고유 값 ()** 함수는 지원 되지 않습니다.  
  
-   데이터 정렬을 제공하는 구문 옵션은 지원되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
