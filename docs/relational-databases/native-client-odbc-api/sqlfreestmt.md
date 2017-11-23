---
title: SQLFreeStmt | Microsoft Docs
ms.custom: 
ms.date: 11/23/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e84e2d33e2c6c6a56b0f69f95091b99c81593f9e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  일반적으로   
      ODBC 3.0 이상에서는**SQLFreeStmt** 가 권장되지 않습니다. 그러나 응용 프로그램에서 문을 다시 사용 해야 하는 경우 사용 해야 **SQLFreeStmt** 와 **SQL_RESET_PARAMS** 및 **SQL_UNBIND** 옵션). 또한 사용 해야 [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md), 및 [ SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 교체 또는 기능을 **SQLFreeStmt** 및 대신 사용 해야 합니다.  
  
 일반적으로 스키마를 삭제 하는 보다 새로 할당 문을 다시 사용 하려면 더 효율적입니다. 문 다시 사용 하는 같은 경우가 SQLFreeStmt 여전히 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLFreeStmt 함수](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
