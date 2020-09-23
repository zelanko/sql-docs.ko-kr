---
title: SQL Server 메시지 결과(OLE DB 드라이버)
description: OLE DB Driver for SQL Server 행 집합 또는 개수를 생성하지 않는 Transact-SQL 문 및 예상되는 반환 값에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc3701313f920eead650435ca40538ad8a4b6ef0
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862501"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하면 OLE DB Driver for SQL Server 행 집합이나 영향을 받는 행 수가 생성되지 않습니다.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 성공적으로 실행되면 OLE DB Driver for SQL Server가 S_OK를 반환하고 OLE DB Driver for SQL Server 소비자가 메시지를 사용할 수 있습니다.  
  
 여러 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하거나 소비자가 OLE DB Driver for SQL Server 멤버 함수를 실행한 후 OLE DB Driver for SQL Server는 S_OK를 반환하며 여기에는 사용 가능한 하나 이상의 정보 메시지가 있습니다.  
  
OLE DB Driver for SQL Server 소비자는 쿼리 텍스트를 동적으로 지정할 수 있습니다. 소비자는 모든 멤버 함수 실행 후 오류 인터페이스를 확인해야 합니다. 반환 코드 값, `IRowset` 또는 `IMultipleResults`에 대한 인터페이스 참조 반환 여부, 영향을 받는 행 수와 관계없이 항상 이 검사를 수행해야 합니다.
  
## <a name="see-also"></a>참고 항목  
 [Errors](../../oledb/ole-db-errors/errors.md)  
  
  
