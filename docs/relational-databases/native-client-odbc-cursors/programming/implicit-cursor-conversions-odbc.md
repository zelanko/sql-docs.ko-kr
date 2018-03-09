---
title: "암시적 커서 변환 (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1f2e8c6ced47894e6e8737641eda36aa33e7d22
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="implicit-cursor-conversions-odbc"></a>암시적 커서 변환(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  응용 프로그램을 통해 커서 유형을 요청한 수 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 다음 요청한 유형의 서버 커서에서 지원 되지 않는 SQL 문을 실행 합니다. 에 대 한 호출 **SQLExecute** 또는 **SQLExecDirect** SQL_SUCCESS_WITH_INFO를 반환 하 고 **SQLGetDiagRec** 반환:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 응용 프로그램 호출 하 여 현재 사용 되 고 커서의 유형을 확인할 수 **SQLGetStmtOption** 에서는 SQL_CURSOR_TYPE로 설정 합니다. 커서 유형 변환은 하나의 문에만 적용됩니다. 다음 **SQLExecDirect** 또는 **SQLExecute** 수행할 수는 원래 문 커서 설정을 사용 하 여 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [커서 프로그래밍 정보 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
