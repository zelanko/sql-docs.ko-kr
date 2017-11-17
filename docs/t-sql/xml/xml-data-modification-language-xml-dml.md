---
title: "XML 데이터 수정 언어 (XML DML) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18fb5825297754c59f2824b6f05150ddaed7bb9c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xml-data-modification-language-xml-dml"></a>XML DML(XML 데이터 수정 언어)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML DML(XML 데이터 수정 언어)은 XQuery 언어의 확장 언어입니다. W3C에 의해 정의된 바와 같이 XQuery 언어에는 DML(데이터 조작 언어) 부분이 부족합니다. 이 항목 및 XQuery 언어에 도입 하는 XML DML 제공 하는 완벽 한 기능의 쿼리 및 데이터 수정 언어에 대해 사용할 수 있는 **xml** 데이터 형식입니다.  
  
 XML DML은 XQuery에 대해 다음과 같은 대/소문자 구분 키워드를 추가합니다.  
  
-   **삽입**  
  
-   **삭제**  
  
-   **replace value o f**  
  
 에 설명 된 대로 [XML 데이터 형식 및 열 &#40; SQL Server &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md), 변수 및 열을 만들 수 있습니다는 **xml** 입력 하 고 XML 문서 또는 조각을을 할당 합니다. 이러한 XML 인스턴스를 수정 또는 업데이트하려면 다음을 수행합니다.  
  
-   사용 하 여는 [modify () 메서드 xml 데이터 형식)](../../t-sql/xml/modify-method-xml-data-type.md) 의 **xml** 데이터 형식입니다.  
  
-   내부의 적절 한 XML DML 문이 지정 된 **modify ()** 메서드.  
  
 일부 특성은 해당 값을 삽입, 삭제 또는 수정할 수 없습니다. 예를 들어  
  
-   형식화 된 또는 형식화 되지 않은 **xml,** 특성은 **xmlns**, **xmlns:\***, 및 **xml:base**합니다.  
  
-   형식화 된 **xml** 특성은만 **xsi: nil**, 및 **xsi: type**합니다.  
  
 다른 제한 사항은 다음과 같습니다.  
  
-   형식화 된 또는 형식화 되지 않은 **xml**, 특성을 삽입할 **xml:base** 실패 합니다.  
  
-   형식화 된 **xml**, 삭제 및 수정 된 **xsi: nil** 특성 실패 합니다. 형식화 되지 않은 **xml**, 특성을 삭제 하거나 해당 값을 수정할 수 있습니다.  
  
-   형식화 된 **xml**의 값을 수정 하는 **xs:type** 특성 실패 합니다. 형식화 되지 않은 **xml**, 특성 값을 수정할 수 있습니다.  
  
 형식화된 XML 인스턴스를 수정하는 경우 최종 형식은 해당 유형의 유효한 인스턴스여야 합니다. 그렇지 않으면 유효성 검사 오류가 반환됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [insert&#40; XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)   
 [delete&#40; XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)   
 [value of &#40; XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)  
  
  

