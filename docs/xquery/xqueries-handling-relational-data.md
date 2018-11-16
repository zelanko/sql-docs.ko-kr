---
title: 관계형 데이터를 처리 하는 XQueries | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9aa8b150a26e64d4a61efe80ab635110e540af33
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51291021"
---
# <a name="xqueries-handling-relational-data"></a>관계형 데이터에 대한 XQuery 처리
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  에 대해 XQuery를 지정 하는 **xml** 유형 열 또는 변수 중 하나를 사용 하 여 합니다 [XML 데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md)합니다. 여기에 포함 됩니다 **query ()** 를 **value ()** 합니다 **exist ()**, 또는 **modify ()** 합니다. XQuery는 XML을 생성하는 쿼리에서 식별된 XML 인스턴스에 대해 실행됩니다.  
  
 XQuery 실행으로 생성된 XML에는 다른 Transact-SQL 변수 또는 행 집합 열로부터 검색된 값이 포함될 수 있습니다. 비-XML 관계형 데이터를 결과 XML에 바인딩하기 위해 SQL Server는 XQuery 확장으로 다음과 같은 의사 함수를 제공합니다.  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 XQuery를 지정할 때 이러한 XQuery 확장을 사용할 수 있습니다 합니다 **query ()** 메서드는 **xml** 데이터 형식입니다. 결과적으로 **query ()** 메서드는 xml에서 및 비 데이터를 결합 하는 XML을 생성할 수 있습니다-**xml** 데이터 형식입니다.  
  
 사용 하는 경우 이러한 함수를 사용할 수도 있습니다는 **xml** 데이터 형식 메서드 **modify ()** 에 **value ()** 를 **query ()**, 및  **exist ()** XML 내 관계형 값을 노출 합니다.  
  
 자세한 내용은 [1!s!sql:column () 함수 (XQuery)](../xquery/xquery-extension-functions-sql-column.md) 하 고 [sql: variable 함수 (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
