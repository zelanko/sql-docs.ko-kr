---
title: 암시적 커서 변환 (ODBC) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e62604404c83e7780d50438a485910e5af4d4f05
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784380"
---
# <a name="implicit-cursor-conversions-odbc"></a>암시적 커서 변환(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  응용 프로그램은 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 를 통해 커서 유형을 요청한 다음 요청한 유형의 서버 커서에서 지원 되지 않는 SQL 문을 실행할 수 있습니다. **Sqlexecute** 또는 **sqlexecdirect** 를 호출 하면 SQL_SUCCESS_WITH_INFO 반환 되 고 **SQLGetDiagRec** 에서 반환 됩니다.  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 응용 프로그램은 SQL_CURSOR_TYPE로 설정 된 **SQLGetStmtOption** 를 호출 하 여 현재 사용 중인 커서 유형을 확인할 수 있습니다. 커서 유형 변환은 하나의 문에만 적용됩니다. 다음 **Sqlexecdirect** 또는 **sqlexecute** 는 원래 문 커서 설정을 사용 하 여 수행 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [커서 프로그래밍 정보 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
