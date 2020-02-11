---
title: 생성자 함수 (XQuery) | Microsoft Docs
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
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f64c9ff6664410983d9c3ce7ebdbf07e493ca03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038996"
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
  
## <a name="remarks"></a>설명  
 생성자는 기본 및 파생 원자 XSD 유형에 대해 지원됩니다. 그러나 **xdt: yearMonthDuration 및 xdt: dayTimeDuration**및 **xs: QName**, **xs: NMTOKEN**및 **xs: NOTATION** 을 포함 하는 **xs: duration**의 하위 유형은 지원 되지 않습니다. 연결된 스키마 컬렉션에서 사용할 수 있는 사용자 정의 원자 유형도 다음 유형으로부터 직접 또는 간접으로 파생될 수 있는 경우 사용할 수 있습니다.  
  
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
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. dateTime() XQuery 함수를 사용하여 이전 제품 설명 검색  
 이 예에서는 **xml** 유형 변수에 샘플 xml 문서를 먼저 할당 합니다. 이 문서에는 <`ProductDescription` `DateCreated`> 자식 요소가 포함 된 세 개의 샘플 <> 요소가 포함 되어 있습니다.  
  
 그런 다음 변수를 쿼리하여 특정 날짜 이전에 생성된 제품 설명만 검색합니다. 비교를 위해 쿼리에서 **xs: dateTime ()** 생성자 함수를 사용 하 여 날짜를 입력 합니다.  
  
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
  
-   ... WHERE 루프 구조를 사용 하 여 WHERE \<절에 지정 된 조건을 충족 하는 제품 설명> 요소를 검색 합니다.  
  
-   **Datetime ()** 생성자 함수는 **datetime** 형식 값을 생성 하는 데 사용 되므로 적절 하 게 비교할 수 있습니다.  
  
-   그런 다음 쿼리가 결과 XML을 생성합니다. 일련의 특성을 생성하기 때문에 쉼표와 괄호가 XML 생성에 사용됩니다.  
  
 다음은 결과입니다.  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>참고 항목  
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
