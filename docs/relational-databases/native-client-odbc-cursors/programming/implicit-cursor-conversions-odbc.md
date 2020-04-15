---
title: 암시적 커서 변환(ODBC) | 마이크로 소프트 문서
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ced726893b0f287db6b1fec7c8d16c6b844eea2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298383"
---
# <a name="implicit-cursor-conversions-odbc"></a>암시적 커서 변환(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  응용 프로그램은 [SQLSetStmtAttr을](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 통해 커서 형식을 요청한 다음 요청된 형식의 서버 커서에서 지원되지 않는 SQL 문을 실행할 수 있습니다. **SQLExecute** 또는 **SQLExecDirect에** 대한 호출은 SQL_SUCCESS_WITH_INFO 반환하고 **SQLGetDiagRec는** 반환합니다.  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 응용 프로그램은 **SQL_CURSOR_TYPE 위해 SQLGetStmtOption** 집합을 호출하여 현재 사용 중인 커서 유형을 확인할 수 있습니다. 커서 유형 변환은 하나의 문에만 적용됩니다. 다음 **SQLExecDirect** 또는 **SQLExecute는** 원래 문 커서 설정을 사용하여 수행됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 프로그래밍 세부 정보](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
