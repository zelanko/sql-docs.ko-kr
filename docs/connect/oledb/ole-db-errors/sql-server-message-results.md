---
title: SQL Server 메시지 결과 | Microsoft Docs
description: SQL Server 메시지 결과
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: dfebd7443b24d09e6bf7696caba5449c1890e0d2
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998285"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하면 SQL Server용 OLE DB 드라이버 행 집합이나 영향을 받는 행 수가 생성되지 않습니다.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 성공적으로 실행되면 OLE DB Driver for SQL Server가 S_OK를 반환하고 OLE DB Driver for SQL Server 소비자가 메시지를 사용할 수 있습니다.  
  
 여러 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하거나 소비자가 OLE DB Driver for SQL Server 멤버 함수를 실행한 후 OLE DB Driver for SQL Server는 S_OK를 반환하며 여기에는 사용 가능한 하나 이상의 정보 메시지가 있습니다.  
  
 쿼리 텍스트의 동적 지정을 허용하는 SQL Server용 OLE DB 드라이버 소비자는 반환 코드 값, 반환된 **IRowset** 또는 **IMultipleResults** 인터페이스 참조가 있는지 여부 또는 영향을 받는 행 수에 관계없이 모든 멤버 함수 실행 후에 오류 인터페이스를 확인해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Errors](../../oledb/ole-db-errors/errors.md)  
  
  
