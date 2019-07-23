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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989323"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버의 구성 요소
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server에 대 한 OLE DB 드라이버에는 다음 구성 요소가 포함 됩니다.  

|구성 요소|설명|  
|---------------|-----------------|  
|msoledbsql.dll|SQL Server 기능에 대 한 모든 OLE DB 드라이버를 포함 하는 DLL (동적 연결 라이브러리) 파일입니다.|  
|msoledbsqlr.rll|SQL Server 라이브러리의 OLE DB 드라이버에 대 한 해당 리소스 파일입니다.|   
|msoledbsql.h|SQL Server에 OLE DB 드라이버를 사용 하는 데 필요한 모든 새 정의가 포함 된 SQL Server 헤더 파일에 대 한 OLE DB 드라이버입니다. 이 헤더 파일은 sqloledb 헤더 파일을 대체 합니다.<br /><br /> 참고: sqloledb를 먼저 정의 하기만 하면 동일한 프로그램에서 msoledbsql 및 sqloledb를 참조할 수 있습니다.|  
|msoledbsql.lib|SQL Server에 대 한 OLE DB 드라이버의 일부인 [Opensqlfilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 함수를 직접 호출 하는 데 필요한 라이브러리 파일입니다.<br /><br /> 참고: 프로그래밍 코드에서 msoledbsql.lib 파일을 참조하는 경우 msoledbsql.lib 파일이 해당 시스템 경로 및 애플리케이션을 사용하는 사용자의 시스템 경로에 있는지 확인해야 합니다.|  

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
