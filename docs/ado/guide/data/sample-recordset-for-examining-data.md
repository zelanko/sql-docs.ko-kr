---
title: 데이터를 검사 하기 위한 샘플 레코드 집합 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1882c5298d92e17a7ddaa165288fddfab7fdb02b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924305"
---
# <a name="sample-recordset-for-examining-data"></a>데이터를 검사하기 위한 샘플 레코드 집합
먼저 Microsoft SQL Server의 Northwind 샘플 데이터에 대해 실행 되는 다음 SQL 쿼리를 사용 하 여 반환 되는 **레코드 집합** 개체를 살펴보겠습니다.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 결과 **레코드 집합** 개체는 다음 표에 표시 된 데이터베이스의 모든 생성을 포함 합니다.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|열혈 삼촌 Bob의 유기적 Dried 배|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle Sauerkraut|45.6000|  
|51|Manjimup Dried 사과|53.0000|  
|74|Tofu 라이프|10.0000|  
  
 이러한 결과를 직접 가져오려면 다음 JScript 예제를 사용해 보세요.  
  
-   [레코드 집합을 반환 하는 JScript 예제](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
