---
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32b1f1185dad9b173c12f3acb232c2426d5db411
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014471"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  일반적으로   
      ODBC 3.0 이상에서는**SQLFreeStmt** 가 권장되지 않습니다. 그러나 응용 프로그램에서 문을 다시 사용 해야 하는 경우 계속 사용 해야 **SQLFreeStmt** 사용 하 여 합니다 **SQL_RESET_PARAMS** 하 고 **SQL_UNBIND** 옵션). 사용할 수도 있습니다 [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)하십시오 [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md), 및 [ SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 바꾸거나의 기능을 복제 하 **SQLFreeStmt** 및 대신 사용 해야 합니다.  
  
 일반적으로 삭제 하는 보다 새로 할당 문을 다시 사용 하려면 더 효율적입니다. 문을 다시 사용과 같은 일부 상황에서 SQLFreeStmt 계속 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLFreeStmt Function](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
