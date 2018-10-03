---
title: true 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 646bcb8058a0a4455c71aecd6a4f907c7dd5f332
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740377"
---
# <a name="boolean-constructor-functions---true-xquery"></a>부울 생성자 함수 - true(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  xs:boolean 값 True를 반환합니다. `xs:boolean("1")`와 같습니다.  
  
## <a name="syntax"></a>구문  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>1. true() XQuery 부울 함수 사용  
 다음 예제 쿼리는 형식화 되지 않은 **xml** 변수입니다. 식의 **value ()** 메서드는 부울 값을 반환 **true ()** "aaa"가 특성 값인 경우. 합니다 **value ()** 메서드는 **xml** 데이터 형식이 부울 값을 비트로 변환 하 고 반환 합니다.  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 다음 예제에서는 쿼리가 지정은 형식화 된에 대 한 **xml** 열입니다. `if` 식은 <`ROOT`> 요소의 형식화된 부울 값을 검사하고 그에 따라 생성된 XML을 반환합니다. 이 예에서는 다음을 수행합니다.  
  
-   xs:boolean 유형의 <`ROOT`> 요소를 정의하는 XML 스키마 컬렉션을 만듭니다.  
  
-   형식화 된 테이블을 만듭니다 **xml** XML 스키마 컬렉션을 사용 하는 열입니다.  
  
-   XML 인스턴스를 열에 저장하고 쿼리합니다.  
  
```  
-- Drop table if exist  
--DROP TABLE T  
--go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="ROOT" type="boolean" nillable="true"/>  
</schema>'  
go  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<ROOT xmlns="QNameXSD">true</ROOT>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare namespace a="QNameXSD";   
   if (/a:ROOT[1] eq true()) then  
       <result>Found boolean true</result>  
   else  
       <result>Found boolean false</result>')  
  
FROM T  
-- result = <result>Found boolean true</result>  
-- Clean up  
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
```  
  
## <a name="see-also"></a>관련 항목  
 [부울 생성자 함수 &#40;XQuery&#41;](http://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)  
  
  
