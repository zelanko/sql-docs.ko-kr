---
title: 이름이 없는 열 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d8fb8fc597fd0562640821769e3314b4f3020bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112900"
---
# <a name="columns-without-a-name"></a>이름이 없는 열
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이름이 없는 열은 인라인됩니다. 예를 들어 계산 열이나 열 별칭을 지정하지 않는 중첩된 스칼라 쿼리는 이름이 없는 열을 생성합니다. **xml** 유형의 열일 경우 해당 데이터 형식 인스턴스의 내용이 삽입됩니다. 그렇지 않을 경우에는 열 내용이 텍스트 노드로 삽입됩니다.  
  
```  
SELECT 2+2  
FOR XML PATH  
```  
  
 이 XML을 생성합니다. 기본적으로 행 집합의 각 행에 대해 결과 XML에 <`row`> 요소가 생성됩니다. 이 동작은 RAW 모드와 동일합니다.  
  
 `<row>4</row>`  
  
 다음 쿼리는 3개의 열로 구성된 행 집합을 반환합니다. 이름이 없는 세 번째 열에는 XML 데이터가 포함됩니다. PATH 모드는 xml 유형의 인스턴스를 삽입합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 다음은 결과의 일부입니다.  
  
```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location ...LocationID="10" ...></MI:Location>
  <MI:Location ...LocationID="20" ...></MI:Location>
  ...
</row>
```

## <a name="see-also"></a>참고 항목  
 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
