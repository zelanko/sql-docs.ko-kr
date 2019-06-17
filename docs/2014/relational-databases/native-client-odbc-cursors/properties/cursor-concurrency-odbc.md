---
title: 커서 동시성 (ODBC) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3101da05e25cf67fda816bd889393bbebe8be3ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711458"
---
# <a name="cursor-concurrency-odbc"></a>커서 동시성(ODBC)
  커서 작업은 커서 유형처럼 응용 프로그램에서 설정한 동시성 옵션의 영향을 받습니다. SQL_ATTR_CONCURRENCY 옵션을 사용 하 여 동시성 옵션 설정이 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)합니다. 동시성 유형은 다음과 같습니다.  
  
-   읽기 전용(SQL_CONCUR_READONLY)  
  
-   값(SQL_CONCUR_VALUES)  
  
-   행 버전(SQL_CONCUR_ROWVER)  
  
-   잠금(SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>관련 항목  
 [커서 속성](cursor-properties.md)  
  
  
