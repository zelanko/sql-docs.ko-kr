---
title: "로컬 이름-에서-QName (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- fn:local-name-from-QName function
- local-name-from-QName function
ms.assetid: fafed718-8c3c-403f-93ee-ec51fc157a6e
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b00ab46352c7f60d4bcc316ca6c41f95dd21d2fa
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>Qname-QName의 로컬 이름와 관련 된 함수
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정 된 QName의 로컬 부분을 나타내는 xs: ncname을 반환 *$arg*합니다. 결과 빈 시퀀스 *$arg* 빈 시퀀스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 로컬 이름이 추출되어야 하는 QName입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
 다음 예제에서는 **local-name-from-qname ()** QName 유형 값에서 로컬 이름 및 네임 스페이스 URI 검색 하려면 함수 부분입니다. 이 예에서는 다음을 수행합니다.  
  
-   XML 스키마 컬렉션을 만듭니다.  
  
-   xml 유형 열이 있는 테이블을 만듭니다. xml 유형은 XML 스키마 컬렉션을 사용하여 형식화됩니다.  
  
-   예제 XML 인스턴스를 테이블에 저장합니다. 사용 하 여 **query ()** 인스턴스에서 QName 유형 값의 로컬 이름 부분을 검색 하 여 쿼리 식에서 xml 데이터 형식의 메서드를 실행 합니다.  
  
```  
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
insert into T values ('<root xmlns="QNameXSD" xmlns:a="http://someURI">a:someLocalName</root>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare default element namespace "QNameXSD"; local-name-from-QName(/root[1])')  
FROM T  
-- Result = someLocalName  
-- You can retrive namespace URI part from the QName using the namespace-uri-from-QName() function  
SELECT xmlCol.query('declare default element namespace "QNameXSD"; namespace-uri-from-QName(/root[1])')  
FROM T  
-- Result = http://someURI  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Qname &#40; 관련 함수 XQuery &#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
