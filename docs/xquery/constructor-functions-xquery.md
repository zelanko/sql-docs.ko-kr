---
title: 생성자 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2ce2bc5e905fe4fa8bd204c850d29b1fa0fdadb0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780071"
---
# <a name="constructor-functions-xquery"></a>생성자 함수(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정된 입력으로부터 생성자 함수는 XSD에 기본 제공되거나 사용자 정의 원자 유형의 항목을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>인수  
 *$strval*  
 변환될 문자열입니다.  
  
 *TYP*  
 기본 제공 XSD 유형입니다.  
  
## <a name="remarks"></a>Remarks  
 생성자는 기본 및 파생 원자 XSD 유형에 대해 지원됩니다. 그러나 하위 **xs: duration**를 포함 하는 **xdt: yearmonthduration and xdt: daytimeduration**, 및 **xs: qname**, **xs:nmtoken**, 및 **xs: notation** 지원 되지 않습니다. 연결된 스키마 컬렉션에서 사용할 수 있는 사용자 정의 원자 유형도 다음 유형으로부터 직접 또는 간접으로 파생될 수 있는 경우 사용할 수 있습니다.  
  
#### <a name="supported-base-types"></a>지원되는 기본 유형  
 다음은 지원되는 기본 유형입니다.  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>지원되는 파생 유형  
 다음은 지원되는 파생 유형입니다.  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 SQL Server는 또한 다음과 같은 방식으로 생성 함수 호출에 대한 상수 계산을 지원합니다.  
  
-   인수가 문자열 리터럴인 경우 식은 컴파일 중에 평가됩니다. 값이 유형 제약 조건에 만족하지 않는 경우 정적 오류가 발생합니다.  
  
-   인수가 다른 유형의 리터럴인 경우 식은 컴파일 중에 평가됩니다. 값이 유형 제약 조건에 만족하지 않는 경우 빈 시퀀스가 반환됩니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>1. dateTime() XQuery 함수를 사용하여 이전 제품 설명 검색  
 이 예제에서는 샘플 XML 문서를 먼저 할당 됩니다는 **xml** 형식 변수입니다. 이 문서에는 3개의 예제 <`ProductDescription`> 요소가 포함되며 각 요소에는 <`DateCreated`> 자식 요소가 포함됩니다.  
  
 그런 다음 변수를 쿼리하여 특정 날짜 이전에 생성된 제품 설명만 검색합니다. 비교를 위해 쿼리에서 사용 합니다 **xs:dateTime()** 생성자 함수는 날짜를 입력 합니다.  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   FOR ... WHERE 루프 구조 검색 되는 \<ProductDescription > WHERE 절에 지정 된 조건을 충족 하는 요소입니다.  
  
-   합니다 **datetime ()** 생성자 함수는 생성 하는 데 사용 됩니다 **dateTime** 적절 하 게 비교할 수 있도록 값을 입력 합니다.  
  
-   그런 다음 쿼리가 결과 XML을 생성합니다. 일련의 특성을 생성하기 때문에 쉼표와 괄호가 XML 생성에 사용됩니다.  
  
 다음은 결과입니다.  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
