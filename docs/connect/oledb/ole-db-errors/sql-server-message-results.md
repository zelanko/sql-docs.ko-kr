---
title: SQL Server 메시지 결과 | Microsoft Docs
description: SQL Server 메시지 결과
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 98d04b56c6e1709e629be46ad00fd3f7b8007a5b
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105999"
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하면 SQL Server용 OLE DB 드라이버 행 집합이나 영향을 받는 행 수가 생성되지 않습니다.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 실행에 성공 하면는 OLE DB Driver for SQL Server S_OK를 반환 하 고 메시지는 OLE DB Driver for SQL Server 소비자를 사용할 수 있습니다.  
  
 OLE DB Driver for SQL Server S_OK를 반환 하며 하나 이상의 정보 제공 용 이므로 사용할 수 있는 메시지의 여러 실행에 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 또는 소비자는 OLE DB Driver for SQL Server 멤버 함수를 실행 합니다.  
  
 쿼리 텍스트의 동적 지정을 허용하는 SQL Server용 OLE DB 드라이버 소비자는 반환 코드 값, 반환된 **IRowset** 또는 **IMultipleResults** 인터페이스 참조가 있는지 여부 또는 영향을 받는 행 수에 관계없이 모든 멤버 함수 실행 후에 오류 인터페이스를 확인해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류](../../oledb/ole-db-errors/errors.md)  
  
  
