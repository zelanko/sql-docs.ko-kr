---
description: SQLFreeStmt
title: SQLFreeStmt | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 956ce78ae72c39e1986955fcc562c4a2472eb4a1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465194"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  일반적으로   
      ODBC 3.0 이상에서는 **SQLFreeStmt** 가 권장되지 않습니다. 그러나 응용 프로그램에서 문을 다시 사용 해야 하는 경우에도 **SQL_RESET_PARAMS** 및 **SQL_UNBIND** 옵션과 함께 **SQLFreeStmt** 를 사용 해야 합니다. [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)및 [sqlfreehandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 을 사용 하 여 **SQLFreeStmt** 의 기능을 대체 하거나 중복 하 고 대신이를 사용 해야 할 수도 있습니다.  
  
 일반적으로 문을 삭제 하 고 새 문을 할당 하는 것 보다 문을 다시 사용 하는 것이 더 효율적입니다. 그러나 문 재사용과 같은 경우에도 SQLFreeStmt를 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLFreeStmt 함수](../../odbc/reference/syntax/sqlfreestmt-function.md)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
