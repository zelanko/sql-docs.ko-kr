---
title: 커서 동시성 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5812ccd677c3135a021e9d111f8b667d93e9b32b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cursor-concurrency-odbc"></a>커서 동시성(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  커서 작업은 커서 유형처럼 응용 프로그램에서 설정한 동시성 옵션의 영향을 받습니다. SQL_ATTR_CONCURRENCY 옵션을 사용 하 여 동시성 옵션을 설정 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다. 동시성 유형은 다음과 같습니다.  
  
-   읽기 전용(SQL_CONCUR_READONLY)  
  
-   값(SQL_CONCUR_VALUES)  
  
-   행 버전(SQL_CONCUR_ROWVER)  
  
-   잠금(SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>관련 항목:  
 [커서 속성](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
