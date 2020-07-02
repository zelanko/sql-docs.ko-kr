---
title: XQuery 프롤로그 | Microsoft Docs
description: 쿼리 처리에 필요한 환경을 만드는 일련의 선언과 정의가 포함 된 XQuery 프롤로그에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
- namespaces [XQuery]
- default namespace declarations
ms.assetid: 03924684-c5fd-44dc-8d73-c6ab90f5e069
author: rothja
ms.author: jroth
ms.openlocfilehash: ece175be7fa0791bf1355ed6020121999d62660b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775481"
---
# <a name="modules-and-prologs---xquery-prolog"></a>모듈 및 프롤로그 - XQuery 프롤로그
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

  XQuery 쿼리는 프롤로그와 본문으로 구성됩니다. XQuery 프롤로그는 쿼리 처리에 필요한 환경을 만드는 일련의 선언 및 정의로 구성됩니다. SQL Server에서 XQuery 프롤로그에는 네임스페이스 선언이 포함될 수 있습니다. XQuery 본문은 의도된 쿼리 결과를 지정하는 일련의 식으로 구성됩니다.  
  
 예를 들어 다음 XQuery는 제조 지침을 XML로 저장 하는 **xml** 유형의 명령 열에 대해 지정 됩니다. 이 쿼리는 작업 센터 위치 `10`에 대한 제조 지침을 검색합니다. `query()` **Xml** 데이터 형식의 메서드는 XQuery를 지정 하는 데 사용 됩니다.  
  
```  
SELECT Instructions.query('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') AS Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   XQuery 프롤로그에는 네임 스페이스 접두사 (AWMI) 선언이 포함 되어 `(namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";` 있습니다.  
  
-   `declare namespace` 키워드는 나중에 쿼리 본문에서 사용되는 네임스페이스 접두사를 정의합니다.  
  
-   `/AWMI:root/AWMI:Location[@LocationID="10"]`은 쿼리 본문입니다.  
  
## <a name="namespace-declarations"></a>네임스페이스 선언  
 네임스페이스 선언은 접두사를 정의하고 다음 쿼리에 표시된 것과 같이 이를 네임스페이스 URI와 연결합니다. 쿼리에서 `CatalogDescription` 는 **xml** 유형 열입니다.  
  
 이 열에 대해 XQuery를 지정할 때 쿼리 프롤로그는 `declare namespace` 선언을 지정하여 접두사 `PD`(제품 설명)를 네임스페이스 URI와 연결합니다. 이 접두사는 쿼리 본문에서 네임스페이스 URI 대신 사용됩니다. 결과 XML의 노드는 네임스페이스URI와 연결된 네임스페이스에 있습니다.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 쿼리 가독성을 향상시키기 위해 `declare namespace`를 사용하여 쿼리 프롤로그에서 접두사와 네임스페이스 바인딩을 선언하는 대신 WITH XMLNAMESPACES를 사용하여 네임스페이스를 선언할 수 있습니다.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
  
SELECT CatalogDescription.query('  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 자세한 내용은 [WITH XMLNAMESPACES를 사용 하 여 쿼리에 네임 스페이스 추가](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)를 참조 하세요.  
  
### <a name="default-namespace-declaration"></a>기본 네임스페이스 선언  
 `declare namespace` 선언을 사용하여 네임스페이스 접두사를 선언하는 대신 `declare default element namespace` 선언을 사용하여 요소 이름에 대해 기본 네임스페이스를 바인딩할 수 있습니다. 이 경우에는 접두사를 지정하지 않습니다.  
  
 다음 예에서 쿼리 본문의 경로 식은 네임스페이스 접두사를 지정하지 않습니다. 기본적으로 모든 요소 이름은 프롤로그에 지정된 기본 네임스페이스에 속합니다.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace  "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
 WITH XMLNAMESPACES를 사용하여 기본 네임스페이스를 선언할 수 있습니다.  
  
```  
WITH XMLNAMESPACES (DEFAULT 'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription')  
SELECT CatalogDescription.query('  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
## <a name="see-also"></a>참고 항목  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)  
  
  
