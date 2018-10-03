---
title: '예제: FOR XML로 생성된 XML에 대한 루트 요소 지정 | Microsoft 문서'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4e59a1c99dfc9bd6de7301764aa5cea2acb0948f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766201"
---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>예제: FOR XML로 생성된 XML에 대한 루트 요소 지정
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  `ROOT` 쿼리에 `FOR XML` 옵션을 지정하면 이 쿼리에 표시된 것과 같이 결과 XML에 대해 단일 최상위 요소를 요청할 수 있습니다. `ROOT` 지시어에 지정된 인수는 루트 요소 이름을 제공합니다.  
  
## <a name="example"></a>예제  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
go  
```  
  
 다음은 결과입니다.  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
