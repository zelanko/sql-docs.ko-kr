---
description: 테이블 이름
title: 테이블 이름 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b264999f800e4387099240526f558110c39e27a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471461"
---
# <a name="table-names"></a>테이블 이름
DBASE, Microsoft Excel, Paradox 또는 텍스트 드라이버를 사용 하는 경우 SELECT 또는 DELETE의 FROM 절에서 발생 하는 테이블 이름 (INSERT에서 INTO 절 이후, UPDATE, CREATE TABLE 및 DROP TABLE은 올바른 경로, 기본 이름 및 파일 이름 확장명을 포함할 수 있습니다.  
  
 SQL 문의 다른 위치에서 테이블 이름 사용은 경로 또는 확장의 사용을 지원 하지 않지만 기본 이름 (예: C:\ABC\EMP의 EMP)만 허용 합니다.  
  
 상관 관계 이름 (별칭)을 사용할 수 있습니다. 다음은 그 예입니다.  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
