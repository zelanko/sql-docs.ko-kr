---
title: 암시적 커서 변환 (ODBC) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eebbfcefdf5c4c9e2d6ed1409e3c119f598a22d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013606"
---
# <a name="implicit-cursor-conversions-odbc"></a>암시적 커서 변환(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  응용 프로그램을 통해 커서 유형을 요청 하 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 다음 요청한 유형의 서버 커서에서 지원 되지 않는 SQL 문을 실행 합니다. 에 대 한 호출 **SQLExecute** 또는 **SQLExecDirect** SQL_SUCCESS_WITH_INFO를 반환 하 고 **SQLGetDiagRec** 반환:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 응용 프로그램 호출 하 여 이제 사용 중인 커서의 유형을 확인할 수 있습니다 **SQLGetStmtOption** 에서는 SQL_CURSOR_TYPE로 설정 합니다. 커서 유형 변환은 하나의 문에만 적용됩니다. 다음 **SQLExecDirect** 또는 **SQLExecute** 수행할 수는 원래 문 커서 설정을 사용 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [커서 프로그래밍 정보 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
