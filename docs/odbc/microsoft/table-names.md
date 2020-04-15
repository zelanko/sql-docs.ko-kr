---
title: 테이블 이름 | 마이크로 소프트 문서
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
ms.openlocfilehash: 91a415cd456186f18ef358b9d504145f78152774
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303124"
---
# <a name="table-names"></a>테이블 이름
dBASE, Microsoft Excel, 역설 또는 텍스트 드라이버를 사용하는 경우 SELECT 또는 DELETE의 FROM 절에서 발생하는 테이블 이름, INSERT의 INTO 절 다음 및 업데이트 후 테이블 만들기 및 DROP 테이블에 유효한 경로, 기본 이름 및 파일 이름 확장자가 포함될 수 있습니다.  
  
 SQL 문의 다른 곳에서 테이블 이름을 사용하는 것은 경로 또는 확장의 사용을 지원하지 않지만 기본 이름(예: EMP FROM C:\ABC\EMP)만 허용합니다.  
  
 상관 관계 이름(별칭)을 사용할 수 있습니다. 다음은 그 예입니다.  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
