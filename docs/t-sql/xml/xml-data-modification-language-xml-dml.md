---
title: XML DML(XML 데이터 수정 언어) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 714e934ebb97a616105321f5921f249752a97dfa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="xml-data-modification-language-xml-dml"></a>XML DML(XML 데이터 수정 언어)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML DML(XML 데이터 수정 언어)은 XQuery 언어의 확장 언어입니다. W3C에 의해 정의된 바와 같이 XQuery 언어에는 DML(데이터 조작 언어) 부분이 부족합니다. 이 항목에서 설명되는 XML DML과 XQuery 언어는 **xml** 데이터 형식에 대해 사용할 수 있는 완벽한 기능의 쿼리 및 데이터 조작 언어를 제공합니다.  
  
 XML DML은 XQuery에 대해 다음과 같은 대/소문자 구분 키워드를 추가합니다.  
  
-   **insert**  
  
-   **delete**  
  
-   **replace value of**  
  
 [XML 데이터 형식 및 열&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)에 설명된 것과 같이 **xml** 형식의 변수 및 열을 만들고 XML 문서 또는 조각을 여기에 할당할 수 있습니다. 이러한 XML 인스턴스를 수정 또는 업데이트하려면 다음을 수행합니다.  
  
-   **xml** 데이터 형식의 [modify() 메서드(xml 데이터 형식)](../../t-sql/xml/modify-method-xml-data-type.md)를 사용합니다.  
  
-   **modify()** 메서드 내부에 적합한 XML DML 문을 지정합니다.  
  
 일부 특성은 해당 값을 삽입, 삭제 또는 수정할 수 없습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
-   형식화된 또는 형식화되지 않은 **xml**의 경우 특성은 **xmlns**, **xmlns:\*** 및 **xml:base**입니다.  
  
-   형식화된 **xml**의 경우 특성은 **xsi:nil** 및 **xsi:type**입니다.  
  
 다른 제한 사항은 다음과 같습니다.  
  
-   형식화된 또는 형식화되지 않은 **xml**의 경우 **xml:base** 특성을 삽입하면 오류가 발생합니다.  
  
-   형식화된 **xml**의 경우 **xsi:nil** 특성을 삭제 및 수정하면 오류가 발생합니다. 형식화되지 않은 **xml**의 경우 특성을 삭제하거나 해당 값을 수정할 수 있습니다.  
  
-   형식화된 **xml**의 경우 **xs:type** 특성의 값을 수정하면 오류가 발생합니다. 형식화되지 않은 **xml**의 경우 특성 값을 수정할 수 있습니다.  
  
 형식화된 XML 인스턴스를 수정하는 경우 최종 형식은 해당 유형의 유효한 인스턴스여야 합니다. 그렇지 않으면 유효성 검사 오류가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [삽입&#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md)   
 [삭제&#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md)   
 [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)  
  
  
