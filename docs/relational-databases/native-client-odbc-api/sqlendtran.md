---
description: SQLEndTran
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd11be29813d5e399d21e35f95afb56507dc165d
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810589"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 **SQLEndTran** 가 작업을 커밋하거나 롤백할 때 문과 연결된 커서를 닫습니다. 서버 커서는 정적 상태가 될 때까지 닫힙니다. **SQLEndTran** 가 작업을 커밋하거나 롤백할 때 문과 연결된 커서의 동작은 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)을 통해 설정된, 드라이버 관련 ODBC 연결 특성인 SQL_COPT_SS_PRESERVE_CURSORS의 값에 의해 결정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 구현 세부 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 함수(SQLEndTran Function)](../../odbc/reference/syntax/sqlendtran-function.md)  
  
