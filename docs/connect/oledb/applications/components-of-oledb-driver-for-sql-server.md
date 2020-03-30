---
title: SQL Server용 OLE DB 드라이버의 구성 요소 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버의 구성 요소
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5a5124519bd95ec02e93a007d9881ec80814cfc8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67989323"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버의 구성 요소
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server에는 다음과 같은 구성 요소들이 포함됩니다.  

|구성 요소|Description|  
|---------------|-----------------|  
|msoledbsql.dll|OLE DB Driver for SQL Server 기능이 모두 포함된 DLL(동적 연결 라이브러리) 파일입니다.|  
|msoledbsqlr.rll|OLE DB Driver for SQL Server 라이브러리에 대한 해당 리소스 파일입니다.|   
|msoledbsql.h|OLE DB Driver for SQL Server를 사용하는 데 필요한 새로운 정의가 모두 포함된 OLE DB Driver for SQL Server 헤더 파일입니다. 이 헤더 파일은 sqloledb.h 헤더 파일을 바꿉니다.<br /><br /> 참고: sqloledb.h가 먼저 정의되어 있는 한, msoledbsql.h 및 sqloledb.h는 동일한 프로그램에서 참조할 수 있습니다.|  
|msoledbsql.lib|OLE DB Driver for SQL Server에 포함된 [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 함수를 직접 호출하는 데 필요한 라이브러리 파일입니다.<br /><br /> 참고: 프로그래밍 코드에서 msoledbsql.lib 파일을 참조하는 경우 msoledbsql.lib 파일이 해당 시스템 경로 및 애플리케이션을 사용하는 사용자의 시스템 경로에 있는지 확인해야 합니다.|  

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
