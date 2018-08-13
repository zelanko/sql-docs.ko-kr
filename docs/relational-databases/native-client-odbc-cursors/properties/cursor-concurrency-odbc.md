---
title: 커서 동시성 (ODBC) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ce47b8c180a413f18e71492dd8d6e141f17b887c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39541093"
---
# <a name="cursor-concurrency-odbc"></a>커서 동시성(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  커서 작업은 커서 유형처럼 응용 프로그램에서 설정한 동시성 옵션의 영향을 받습니다. SQL_ATTR_CONCURRENCY 옵션을 사용 하 여 동시성 옵션을 설정 하는 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). 동시성 유형은 다음과 같습니다.  
  
-   읽기 전용(SQL_CONCUR_READONLY)  
  
-   값(SQL_CONCUR_VALUES)  
  
-   행 버전(SQL_CONCUR_ROWVER)  
  
-   잠금(SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>관련 항목  
 [커서 속성](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
