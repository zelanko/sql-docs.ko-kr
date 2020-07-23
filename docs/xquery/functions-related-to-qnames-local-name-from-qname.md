---
title: 로컬 이름-QName (XQuery) | Microsoft Docs
description: 로컬 이름-QName () 함수를 사용 하 여 QName의 로컬 이름 부분을 반환 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name-from-QName function
- local-name-from-QName function
ms.assetid: fafed718-8c3c-403f-93ee-ec51fc157a6e
author: rothja
ms.author: jroth
ms.openlocfilehash: bc416f49610aa5641aa06d8e3fbd7f6da89c7977
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86901971"
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>QNames 관련 함수 - local-name-from-QName
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  *$Arg*에 지정 된 QName의 로컬 부분을 나타내는 XS: NCNAME을 반환 합니다. *$Arg* 빈 시퀀스인 경우 결과는 빈 시퀀스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 로컬 이름이 추출되어야 하는 QName입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 합니다.  
  
 다음 예제에서는 로컬 이름- **qname ()** 함수를 사용 하 여 qname 형식 값에서 로컬 이름 및 네임 스페이스 URI 부분을 검색 합니다. 이 예에서는 다음을 수행합니다.  
  
-   XML 스키마 컬렉션을 만듭니다.  
  
-   xml 유형 열이 있는 테이블을 만듭니다. xml 유형은 XML 스키마 컬렉션을 사용하여 형식화됩니다.  
  
-   예제 XML 인스턴스를 테이블에 저장합니다. Xml 데이터 형식의 **query ()** 메서드를 사용 하 여 쿼리 식이 실행 되어 인스턴스에서 QName 유형 값의 로컬 이름 부분을 검색 합니다.  
  
```sql
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<root xmlns="QNameXSD" xmlns:a="https://someURI">a:someLocalName</root>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare default element namespace "QNameXSD"; local-name-from-QName(/root[1])')  
FROM T  
-- Result = someLocalName  
-- You can retrieve namespace URI part from the QName using the namespace-uri-from-QName() function  
SELECT xmlCol.query('declare default element namespace "QNameXSD"; namespace-uri-from-QName(/root[1])')  
FROM T  
-- Result = https://someURI  
```  
  
## <a name="see-also"></a>참고 항목  
 [Qname &#40;XQuery&#41;와 관련 된 함수](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
