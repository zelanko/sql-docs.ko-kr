---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d72d7868d0e19719ea7992bdb8ccd1f61f3718d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633168"
---
# <a name="table-names"></a>테이블 이름
경우 dBASE, Microsoft Excel, Paradox, 또는 드라이버를 사용 하는 텍스트, 테이블 이름에서에서 발생 하는 SELECT 또는 DELETE FROM 절은 INSERT INTO 절은 후 업데이트를 CREATE TABLE 및 DROP TABLE 올바른 경로 포함할 수 있습니다, 기본 이름 및 파일 이름 확장명 .  
  
 SQL 문에서 다른 곳에서 테이블 이름 사용 경로 또는 확장의 사용을 지원 하지 않지만 기본 이름 (예를 들어 EMP에서 C:\ABC\EMP)만 허용 됩니다.  
  
 상관 관계 이름 (별칭)을 사용할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
