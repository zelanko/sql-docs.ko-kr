---
title: OLE DB Driver for SQL Server의 구성 요소 | Microsoft Docs
description: OLE DB Driver for SQL Server의 구성 요소
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18b0f0e13fefefe5e3be09d7538150cfccbfcb21
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server의 구성 요소
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server는 다음 구성 요소가 포함 되어 있습니다.  

|구성 요소|Description|  
|---------------|-----------------|  
|msoledbsql.dll|OLE DB driver for SQL Server 기능 모두 포함 하는 동적 연결 라이브러리 (DLL) 파일입니다.|  
|msoledbsqlr.rll|OLE DB 드라이버에서 SQL Server 라이브러리에 대 한 해당 리소스 파일입니다.|   
|msoledbsql.h|OLE DB Driver for SQL Server OLE DB 드라이버를 사용 하는 데 필요한 새 정의 모두 포함 된 SQL Server 헤더 파일에 대 한 합니다. 이 헤더 파일을 sqloledb.h 헤더 파일을 바꿉니다.<br /><br /> 참고: 참조할 수 있습니다 msoledbsql.h 및 동일한 프로그램에 sqloledb.h로 sqloledb.h를 먼저 정의 합니다.|  
|msoledbsql.lib|호출을 직접 데 필요한 라이브러리 파일의 **bcp** 는 OLE DB Driver for SQL Server의 일부인 유틸리티 함수입니다.<br /><br /> 참고: msoledbsql.lib 파일 프로그래밍 코드에서를 참조 하는 경우 필요한 msoledbsql.dll 파일이 해당 시스템 경로 및 확인 하는 사용자의 시스템 경로에 있는지 확인 하려면 응용 프로그램을 사용 합니다.|  

## <a name="see-also"></a>관련 항목:  
 [SQL Server 용 OLE DB 드라이버 빌딩 응용 프로그램](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
