---
title: "테이블 이름 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69af01ea73bfe8ad4f69cb9cae72e8579979ba61
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="table-names"></a>테이블 이름
때 dBASE, Microsoft Excel, Paradox, 또는 드라이버를 사용 하는 텍스트, 테이블 이름에서에서 발생 하는 SELECT 또는 DELETE FROM 절에서 INSERT INTO 절 뒤와 업데이트 후, CREATE TABLE 및 DROP TABLE 올바른 경로 포함할 수 있습니다, 주 이름 및 파일 이름 확장명 .  
  
 SQL 문에서 다른 위치에서 테이블 이름 사용 경로 또는 확장 프로그램의 사용을 지원 하지 않고 기본 이름 (예를 들어 EMP에서 C:\ABC\EMP)만 허용 됩니다.  
  
 상관 관계 이름 (별칭)을 사용할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
