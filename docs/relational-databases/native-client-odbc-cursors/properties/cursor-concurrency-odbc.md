---
title: "커서 동시성 (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc203adcfde52484c013a4cda0483d95511e1cd9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
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
  
  
