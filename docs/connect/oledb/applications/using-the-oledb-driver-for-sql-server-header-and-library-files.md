---
title: SQL Server 헤더 및 라이브러리 파일에 대 한 OLE DB 드라이버를 사용 하 여 | Microsoft Docs
description: SQL Server 헤더 및 라이브러리 파일에 대 한 OLE DB 드라이버를 사용 하 여
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8ed2d5385806ee439cc67111c83cc08ea786e160
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>OLE DB 드라이버를 사용 하 여 SQL Server 헤더 및 라이브러리 파일
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 헤더 및 라이브러리 파일은 설치 과정에서 OLE DB 드라이버에서 SQL Server SDK 옵션을 선택한 경우 설치 됩니다. 응용 프로그램을 개발할 때는 개발에 필요한 모든 파일을 사용자의 개발 환경으로 복사하고 설치해야 합니다. 설치 하 고 SQL Server 용 OLE DB Driver를 재배포 하는 방법에 대 한 자세한 내용은 참조 [설치 OLE DB Driver for SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)합니다.  
  
 OLE DB Driver for SQL Server 헤더 및 라이브러리 파일은 다음 위치에 설치 됩니다.  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\180\SDK  
  
 사용자 지정 응용 프로그램에 SQL Server 데이터 액세스 기능에 대 한 OLE DB 드라이버를 추가 하는 OLE DB Driver for SQL Server 헤더 파일 (msoledbsql.h)를 사용할 수 있습니다. 에 도입 된 새로운 기능을 활용 하는 데 필요한 인터페이스 및 정의 특성, 속성의 모든 OLE DB 드라이버에서 SQL Server 헤더 파일 포함 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다.  
  
 OLE DB 드라이버 SQL Server 헤더 파일 외에도 이기도 되는 내보내기 라이브러리인 msoledbsql.lib 라이브러리 파일에 대 한 [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 기능입니다.  
  
 OLE DB 드라이버에서 SQL Server 헤더 파일은와 Microsoft 데이터 액세스 구성 요소 (MDAC)를 사용 하는 sqloledb.h 헤더 파일 이전 버전과 호환 되지만 SQLOLEDB에 대 한 Clsid를 포함 하지 않습니다 (OLE DB provider에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] MDAC에 포함 된)에 대해 기호 또는 XML 기능이 (지원 되지 않음 OLE DB 드라이버에서 SQL Server 용)이 표시 됩니다.    
  
 SQL Server 용 OLE DB 드라이버를 사용 하는 OLE DB 응용 프로그램 msoledbsql.h 참조 해야 합니다. 응용 프로그램 MDAC (SQLOLEDB)와 OLE DB Driver for SQL Server를 사용할 sqloledb.h 및 msoledbsql.h을 모두 참조할 수 있지만 sqloledb.h에 대 한 참조 먼저와 야 합니다.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>SQL Server 헤더 파일에 대 한 OLE DB 드라이버를 사용 하 여  
 SQL Server 헤더 파일에 대 한 OLE DB 드라이버를 사용 하려면 사용 해야 합니다는 **포함** C/c + + 프로그래밍 코드 내에 문의 합니다. 다음 섹션에는이 OLE DB 응용 프로그램 작업을 수행 하는 방법을 설명 합니다.  
  
> [!NOTE]  
>  OLE DB 드라이버에서 SQL Server 헤더 및 라이브러리 파일에는 Visual Studio c + + 2012를 사용 하 여 컴파일된 이상 수만 있습니다.  
  
### <a name="ole-db"></a>OLE DB  
 사용 하려면 OLE DB Driver 프로그래밍 코드의 다음 줄을 사용 하 여 OLE DB 응용 프로그램에서 SQL Server 헤더 파일:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  응용 프로그램에 있는 경우는 **포함** sqloledb.h에 대 한 문을 **포함** msoledbsql.h에 대 한 문이 그 뒤에 야 합니다.  
  
 SQL Server 용 OLE DB 드라이버를 통해 데이터 원본에 대 한 연결을 만들 때 "MSOLEDBSQL"의 공급자 이름 문자열을 사용 합니다.  

  
## <a name="component-names-and-properties-by-version"></a>버전별 구성 요소 이름 및 속성  

|속성|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 헤더 파일 이름|msoledbsql.h|Sqloledb.h|  
|OLE DB Provider DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>정적 연결 및 BCP 함수  
 응용 프로그램에서 BCP 함수를 사용하는 경우 응용 프로그램의 연결 문자열에 응용 프로그램을 컴파일하는 데 사용된 헤더 파일 및 라이브러리가 함께 제공되는 동일한 버전의 드라이버를 지정해야 합니다.  
  
 자세한 내용은 참조 공연 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
