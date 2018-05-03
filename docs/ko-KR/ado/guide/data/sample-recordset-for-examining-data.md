---
title: 레코드 집합 데이터를 검사 하기 위한 샘플 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ef5f516bb89bb17efef04a89146a518c924f09d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sample-recordset-for-examining-data"></a>데이터를 검사 하기 위한 샘플 레코드 집합
첫째, 살펴보겠습니다는 **레코드 집합** Microsoft SQL Server에서 기본 Northwind 샘플 데이터에 대해 실행에서 다음 SQL 쿼리를 사용 하 여 반환 된 개체입니다.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 결과 **레코드 집합** 개체는 다음 표에 표시 된 데이터베이스의 모든 생성을 포함 합니다.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|유기적 건과 (배)|30.0000|  
|14|두 부|23.2500|  
|28|Rssle 사워크라우트 맛|45.6000|  
|51|나 주 배|53.0000|  
|74|유미 두 부|10.0000|  
  
 이러한 결과 직접 확보 하려는 경우 다음 JScript 예제를 시도해 보십시오.  
  
-   [레코드 집합을 반환 하려면 JScript 예제](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
