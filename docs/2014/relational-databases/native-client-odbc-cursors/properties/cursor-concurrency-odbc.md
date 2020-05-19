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
manager: craigg
ms.openlocfilehash: 7139ace2498ef2eeddb173950281ac4cf493efad
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705590"
---
# <a name="cursor-concurrency-odbc"></a>커서 동시성(ODBC)
  커서 작업은 커서 유형처럼 애플리케이션에서 설정한 동시성 옵션의 영향을 받습니다. 동시성 옵션은 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)의 SQL_ATTR_CONCURRENCY 옵션을 사용 하 여 설정 됩니다. 동시성 유형은 다음과 같습니다.  
  
-   읽기 전용(SQL_CONCUR_READONLY)  
  
-   값(SQL_CONCUR_VALUES)  
  
-   행 버전(SQL_CONCUR_ROWVER)  
  
-   잠금(SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>참고 항목  
 [커서 속성](cursor-properties.md)  
  
  
