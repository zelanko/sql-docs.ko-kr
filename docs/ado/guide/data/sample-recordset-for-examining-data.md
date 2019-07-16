---
title: 레코드 집합 데이터를 검사 하는 것에 대 한 샘플 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924305"
---
# <a name="sample-recordset-for-examining-data"></a>데이터를 검사하기 위한 샘플 레코드 집합
먼저 살펴보겠습니다 합니다 **레코드 집합** Microsoft SQL Server의 기본 Northwind 샘플 데이터에 대 한 실행에서 다음 SQL 쿼리를 사용 하 여 반환 된 개체입니다.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 결과 **레코드 집합** 개체는 다음 표에 나와 있는 데이터베이스의 모든 생성을 포함 합니다.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|대양 유기적 건과 (배)|30.0000|  
|14|두 부|23.2500|  
|28|Rssle 사워크라우트|45.6000|  
|51|나 주 배|53.0000|  
|74|유미 두 부|10.0000|  
  
 사용자가 직접 이러한 결과 얻는 데 관심이 있다면 다음 JScript 예제를 시도해 보십시오.  
  
-   [레코드 집합을 반환할 JScript 예제](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
