---
title: 로컬-이름-에서-QName (XQuery) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 237db63c04d9b5a241bcabbca5a45e054da03118
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661942"
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>QNames 관련 함수 - local-name-from-QName
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정 된 QName의 로컬 부분을 나타내는 ncname을 반환 *$arg*합니다. 결과 빈 시퀀스 *$arg* 빈 시퀀스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 로컬 이름이 추출되어야 하는 QName입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
 다음 예제에서는 합니다 **local-name-from-qname ()** QName 유형 값에서 파트를 로컬 이름과 네임 스페이스 URI 검색 하는 함수입니다. 이 예에서는 다음을 수행합니다.  
  
-   XML 스키마 컬렉션을 만듭니다.  
  
-   xml 유형 열이 있는 테이블을 만듭니다. xml 유형은 XML 스키마 컬렉션을 사용하여 형식화됩니다.  
  
-   예제 XML 인스턴스를 테이블에 저장합니다. 사용 하는 **query ()** 인스턴스에서 QName 유형 값의 로컬 이름 부분을 검색할 xml 데이터 형식, 쿼리 식의 메서드를 실행 합니다.  
  
```sql
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
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
  
## <a name="see-also"></a>관련 항목  
 [QNames 관련 함수 &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
