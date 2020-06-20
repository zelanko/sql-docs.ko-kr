---
title: 커서 동시성 (ODBC) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c47f24152978fedf8f2c3d49ec3b721969712814
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020588"
---
# <a name="cursor-concurrency-odbc"></a>커서 동시성(ODBC)
  커서 작업은 커서 유형처럼 애플리케이션에서 설정한 동시성 옵션의 영향을 받습니다. 동시성 옵션은 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)의 SQL_ATTR_CONCURRENCY 옵션을 사용 하 여 설정 됩니다. 동시성 유형은 다음과 같습니다.  
  
-   읽기 전용(SQL_CONCUR_READONLY)  
  
-   값(SQL_CONCUR_VALUES)  
  
-   행 버전(SQL_CONCUR_ROWVER)  
  
-   잠금(SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>참고 항목  
 [커서 속성](cursor-properties.md)  
  
  
