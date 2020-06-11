---
title: 관계형 데이터를 처리 하는 XQueries | Microsoft Docs
description: 'XQuery 확장 sql: column () 및 sql: variable ()을 사용 하 여 비 XML 관계형 데이터를 XML에 바인딩하는 방법에 대해 알아봅니다.'
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
ms.openlocfilehash: e9f1e69c10e4930a4a039528cffc4dbb13a67548
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689477"
---
# <a name="xqueries-handling-relational-data"></a>관계형 데이터에 대한 XQuery 처리
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Xml [데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md)중 하나를 사용 하 여 **xml** 유형의 열 또는 변수에 대해 XQuery를 지정 합니다. 여기에는 **query ()**, **value ()**, **exist ()** 또는 **modify ()** 가 포함 됩니다. XQuery는 XML을 생성하는 쿼리에서 식별된 XML 인스턴스에 대해 실행됩니다.  
  
 XQuery 실행으로 생성된 XML에는 다른 Transact-SQL 변수 또는 행 집합 열로부터 검색된 값이 포함될 수 있습니다. 비-XML 관계형 데이터를 결과 XML에 바인딩하기 위해 SQL Server는 XQuery 확장으로 다음과 같은 의사 함수를 제공합니다.  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 **Xml** 데이터 형식의 **query ()** 메서드에서 xquery를 지정할 때 이러한 xquery 확장을 사용할 수 있습니다. 따라서 **query ()** 메서드는 xml 및 비-**xml** 데이터 형식의 데이터를 결합 하는 xml을 생성할 수 있습니다.  
  
 **Xml** 데이터 형식 메서드 **modify ()**, **value ()**, **query ()** 및 **exist ()** 를 사용 하 여 xml 내에 관계형 값을 노출 하는 경우에도 이러한 함수를 사용할 수 있습니다.  
  
 자세한 내용은 [sql: column () 함수 (xquery)](../xquery/xquery-extension-functions-sql-column.md) 및 [sql: variable () 함수 (xquery)](../xquery/xquery-extension-functions-sql-variable.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
