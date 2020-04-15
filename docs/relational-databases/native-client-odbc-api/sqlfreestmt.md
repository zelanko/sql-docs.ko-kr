---
title: SQLFreeStmt | 마이크로 소프트 문서
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3eb86f9b7b1076fa3a01135b5780637ee9857f90
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298464"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  일반적 으로   
      ODBC 3.0 이상에서는**SQLFreeStmt** 가 권장되지 않습니다. 그러나 응용 프로그램이 문을 다시 사용해야 하는 경우에도 **SQL_RESET_PARAMS** 및 **SQL_UNBIND** 옵션)과 함께 **SQLFreeStmt를** 사용해야 합니다. [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBind매개 변수,](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) [SQLBindCol,](../../relational-databases/native-client-odbc-api/sqlbindcol.md) [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)및 [SQLFreeHandle을](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 사용하여 **SQLFreeStmt의** 함수를 대체하거나 복제할 수 있으며 대신 사용해야 합니다.  
  
 일반적으로 문을 삭제하고 새 문을 할당하는 것보다 문을 재사용하는 것이 더 효율적입니다. 그러나 문 재사용과 같은 일부 상황에서는 SQLFreeStmt를 계속 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLFreeStmt 함수](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
