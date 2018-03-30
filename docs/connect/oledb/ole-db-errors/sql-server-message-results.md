---
title: SQL Server 메시지 결과 | Microsoft Docs
description: SQL Server 메시지 결과
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 71036d3e97fcaf13f11f4e9fda741b9983902039
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="sql-server-message-results"></a>SQL Server 메시지 결과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행할 때 영향을 받는 행의 개수 또는 SQL Server 행 집합에 대 한 OLE DB 드라이버를 생성 하지 않습니다.  
  
-   PRINT  
  
-   심각도가 10 이하인 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 이러한 문은 하나 이상의 정보 메시지를 반환하거나, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 행 집합이나 개수 결과 대신 정보 메시지를 반환하도록 합니다. 실행에 성공는 OLE DB Driver for SQL Server S_OK를 반환 하며, 메시지는 OLE DB driver for SQL Server 소비자는 사용할 수 있습니다.  
  
 OLE DB Driver for SQL Server는 S_OK를 반환 되었으며 하나 이상의 정보 메시지는 여러 실행 후 사용 가능한 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 또는 소비자는 OLE DB Driver for SQL Server 멤버 함수를 실행 합니다.  
  
 OLE DB 드라이버에서 쿼리 텍스트의 동적 지정을 허용 하는 SQL Server 소비자의 반환 코드, 유무는 반환 값에 관계 없이 모든 멤버 함수 실행 후 오류 인터페이스를 확인 해야 **IRowset** 또는 **IMultipleResults** 인터페이스 참조 또는 영향을 받는 행 수입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [오류](../../oledb/ole-db-errors/errors.md)  
  
  
