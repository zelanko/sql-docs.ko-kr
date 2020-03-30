---
title: SQL Server용 OLE DB 드라이버 헤더 및 라이브러리 파일 사용 | Microsoft Docs
description: SQL Server 헤더 및 라이브러리 파일용 OLE DB 드라이버 사용
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
ms.openlocfilehash: 93b906a0604772fe224b1e63eaf6eed9eb8af983
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67989228"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>SQL Server 헤더 및 라이브러리 파일용 OLE DB 드라이버 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  설치 중에 OLE DB Driver for SQL Server SDK 옵션이 선택되면 OLE DB Driver for SQL Server 헤더 및 라이브러리 파일이 설치됩니다. 애플리케이션을 개발할 때는 개발에 필요한 모든 파일을 사용자의 개발 환경으로 복사하고 설치해야 합니다. OLE DB Driver for SQL Server의 설치 및 재배포 방법에 대한 자세한 내용은 [OLE DB Driver for SQL Server 설치](../../oledb/applications/installing-oledb-driver-for-sql-server.md)를 참조하세요.  
  
 OLE DB Driver for SQL Server 헤더 및 라이브러리 파일은 다음 위치에 설치됩니다.  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 OLE DB Driver for SQL Server 헤더 파일(msoledbsql.h)은 OLE DB Driver for SQL Server 데이터 액세스 기능을 사용자가 지정한 애플리케이션에 추가하는 데 사용할 수 있습니다. SQL Server용 OLE DB 드라이버 헤더 파일에는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새로운 기능을 활용하는 데 필요한 모든 정의, 특성, 속성 및 인터페이스가 포함되어 있습니다.  
  
 OLE DB Driver for SQL Server 헤더 파일에 더해 which is the export library for [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 기능에 대한 내보내기 라이브러리인 msoledbsql.lib 라이브러리 파일도 있습니다.  
  
 SQL Server용 OLE DB 드라이버 헤더 파일은 Microsoft Data Access Components(MDAC)에서 사용되는 sqloledb.h 헤더 파일과 호환되지만 SQLOLEDB(MDAC에 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 OLE DB 공급자)에 사용되는 CLSID 또는 XML 기능(SQL Server용 OLE DB Driver에서 지원되지 않음)에 사용되는 기호는 포함하지 않습니다.    
  
 OLE DB Driver for SQL Server를 사용하는 OLE DB 애플리케이션은 msoledbsql.h 참조만 필요합니다. MDAC(SQLOLEDB)와 SQL Server용 OLE DB 드라이버를 모두 사용하는 애플리케이션은 sqloledb.h 및 msoledbsql.h를 모두 참조할 수 있지만 sqloledb.h를 먼저 참조해야 합니다.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>OLE DB Driver for SQL Server 헤더 파일 사용  
 OLE DB Driver for SQL Server 헤더 파일을 사용하려면 사용자의 C/C++ 프로그래밍 코드 내에 **include** 문을 사용해야 합니다. 다음 섹션에서는 OLE DB 애플리케이션에서 이 작업을 어떻게 수행할 수 있을지 설명합니다.  
  
> [!NOTE]  
>  OLE DB Driver for SQL Server 헤더 및 라이브러리 파일은 Visual Studio C++ 2012 이상을 사용해야 컴파일할 수 있습니다.  
  
### <a name="ole-db"></a>OLE DB  
 OLE DB 애플리케이션에서 OLE DB Driver for SQL Server 헤더 파일을 사용하려면 다음 프로그래밍 코드 행을 사용합니다.  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  애플리케이션에 sqloledb.h에 대한 **include** 문이 있는 경우 msoledbsql.h에 대한 **include** 문이 그 다음에 와야 합니다.  
  
 OLE DB Driver for SQL Server를 통해 데이터 원본에 대한 연결을 만들 때 공급자 이름 문자열에는 "MSOLEDBSQL"을 사용합니다.  

  
## <a name="component-names-and-properties-by-version"></a>버전별 구성 요소 이름 및 속성  

|속성|SQL Server용 OLE DB 드라이버|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 헤더 파일 이름|msoledbsql.h|Sqloledb.h|  
|OLE DB Provider DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>정적 연결 및 BCP 함수  
 애플리케이션에서 BCP 함수를 사용하는 경우 애플리케이션의 연결 문자열에 애플리케이션을 컴파일하는 데 사용된 헤더 파일 및 라이브러리가 함께 제공되는 동일한 버전의 드라이버를 지정해야 합니다.  
  
 자세한 내용은 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
