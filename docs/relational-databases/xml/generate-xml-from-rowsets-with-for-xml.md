---
title: 행 집합으로부터 XML을 생성하기 위해 FOR XML 사용 | Microsoft 문서
description: TYPE 지시문을 FOR XML 절과 함께 사용하여 행 집합에서 xml 데이터 형식 인스턴스를 생성하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a3db0a22d7bcba85d77979383c004f0834fe422
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85691241"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>행 집합으로부터 XML을 생성하기 위해 FOR XML 사용
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  새로운 **TYPE** 지시어로 FOR XML을 사용하여 행 집합으로부터 **xml** 데이터 형식의 인스턴스를 생성할 수 있습니다.  
  
 결과는 **xml** 데이터 형식의 열, 변수 또는 매개 변수에 할당할 수 있습니다. 또한 FOR XML은 계층적 구조를 생성하도록 중첩될 수 있습니다. 이로 인해 FOR XML EXPLICIT보다 중첩된 FOR XML이 작성하기에 더욱 편리하지만 중첩이 많은 계층에서는 성능이 저하될 수 있습니다. FOR XML은 또한 새로운 PATH 모드를 제공합니다. 이 새로운 모드는 열 값이 나타나는 XML 트리의 경로를 지정합니다.  
  
 새로운 **FOR XML TYPE** 지시어를 사용하여 SQL 구문에서 관계형 데이터에 대해 읽기 전용 XML 뷰를 정의할 수 있습니다. 이 뷰는 다음 예에서와 같이 SQL 문과 포함된 XQuery에서 쿼리할 수 있습니다. 또한 저장 프로시저에서 이러한 SQL 뷰를 참조할 수도 있습니다.  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>예제: 생성된 xml 데이터 형식을 반환하는 SQL 뷰  
 다음 SQL 뷰 정의는 XML 열로부터 검색된 관계형 열, pk 및 책 저자에 대해 XML 뷰를 만듭니다.  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 V 뷰에는 XML 유형의 단일 columnxmlVal이 있는 단일 행이 포함됩니다`.` 이 뷰는 일반적인 **xml** 데이터 형식 인스턴스와 같이 쿼리될 수 있습니다. 예를 들어 다음 쿼리는 이름이 "David"인 저자를 반환합니다.  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 SQL 뷰 정의는 주석 지정 스키마를 사용하여 만든 XML 뷰와 일부 비슷합니다. 하지만 여기에는 중요한 차이가 있습니다. SQL 뷰 정의는 읽기 전용이며 포함된 XQuery로 조작되어야 합니다. XML 뷰는 주석 지정 스키마를 사용하여 생성됩니다. 또한 SQL 뷰는 XQuery 식을 적용하기 전에 XML 결과를 구체화하지만 XML 뷰의 XPath 쿼리는 기본 테이블에서 SQL 쿼리를 평가합니다.  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
