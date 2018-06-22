---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 389236f4ede54ac618bac6d9d0fd0687c61a12e4
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35700494"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLCloseCursor** 대체 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 와 *옵션* SQL_CLOSE의 값입니다. 수신 시 **SQLCloseCursor**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 보류 중인 결과 집합 행을 삭제 합니다. 문의 열 및 매개 변수 바인딩(있는 경우)은 **SQLCloseCursor**에 의해 변경되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLCloseCursor](http://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
