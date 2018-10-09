---
title: SQL Server용 Microsoft OLE DB 드라이버 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 164b87135257f812898c254fd7fd4f5c762c72ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735251"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버의 구성 요소
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  다음 구성 요소를 포함 하는 OLE DB Driver for SQL Server:  

|구성 요소|설명|  
|---------------|-----------------|  
|msoledbsql.dll|OLE DB driver for SQL Server 기능이 모두 포함 하는 동적 연결 라이브러리 (DLL) 파일입니다.|  
|msoledbsqlr.rll|OLE DB Driver for SQL Server 라이브러리에 대 한 함께 제공 되는 리소스 파일입니다.|   
|msoledbsql.h|OLE DB 드라이버 새 정의가 모두 포함 하는 SQL Server 헤더 파일에 대 한 SQL Server 용 OLE DB 드라이버를 사용 하려면 필요 합니다. 이 헤더 파일 sqloledb.h 헤더 파일을 대체합니다.<br /><br /> 참고: 참조할 수 있습니다 msoledbsql.h 및 동일한 프로그램에 sqloledb.h로 sqloledb.h를 먼저 정의 됩니다.|  
|msoledbsql.lib|라이브러리 파일 하는 데 필요한 직접 호출 합니다 [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) OLE DB driver for SQL Server에 포함 된 함수입니다.<br /><br /> 참고: 프로그래밍 코드에서 msoledbsql.lib 파일을 참조하는 경우 msoledbsql.lib 파일이 해당 시스템 경로 및 응용 프로그램을 사용하는 사용자의 시스템 경로에 있는지 확인해야 합니다.|  

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
