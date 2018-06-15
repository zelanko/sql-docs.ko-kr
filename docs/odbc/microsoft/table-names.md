---
title: 테이블 이름 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 53942dbfedbc630962fe49675620c47ad7e32b2a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906088"
---
# <a name="table-names"></a>테이블 이름
때 dBASE, Microsoft Excel, Paradox, 또는 드라이버를 사용 하는 텍스트, 테이블 이름에서에서 발생 하는 SELECT 또는 DELETE FROM 절에서 INSERT INTO 절 뒤와 업데이트 후, CREATE TABLE 및 DROP TABLE 올바른 경로 포함할 수 있습니다, 주 이름 및 파일 이름 확장명 .  
  
 SQL 문에서 다른 위치에서 테이블 이름 사용 경로 또는 확장 프로그램의 사용을 지원 하지 않고 기본 이름 (예를 들어 EMP에서 C:\ABC\EMP)만 허용 됩니다.  
  
 상관 관계 이름 (별칭)을 사용할 수 있습니다. 예를 들어:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
