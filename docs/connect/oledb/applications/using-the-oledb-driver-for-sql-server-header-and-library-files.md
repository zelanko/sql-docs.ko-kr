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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989228"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>SQL Server 헤더 및 라이브러리 파일용 OLE DB 드라이버 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 헤더 및 라이브러리 파일에 대 한 OLE DB 드라이버는 설치 프로세스 중에 SQL Server SDK 용 OLE DB 드라이버 옵션을 선택 하면 설치 됩니다. 애플리케이션을 개발할 때는 개발에 필요한 모든 파일을 사용자의 개발 환경으로 복사하고 설치해야 합니다. SQL Server 용 OLE DB 드라이버를 설치 하 고 재배포 하는 방법에 대 한 자세한 내용은 [SQL Server에 대 한 OLE DB 드라이버 설치](../../oledb/applications/installing-oledb-driver-for-sql-server.md)를 참조 하세요.  
  
 SQL Server 헤더 및 라이브러리 파일에 대 한 OLE DB 드라이버는 다음 위치에 설치 됩니다.  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 SQL Server 헤더 파일 (msoledbsql)에 대 한 OLE DB 드라이버를 사용 하 여 사용자 지정 응용 프로그램에 SQL Server 데이터 액세스 기능을 위한 OLE DB 드라이버를 추가할 수 있습니다. SQL Server용 OLE DB 드라이버 헤더 파일에는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새로운 기능을 활용하는 데 필요한 모든 정의, 특성, 속성 및 인터페이스가 포함되어 있습니다.  
  
 SQL Server 헤더 파일에 대 한 OLE DB 드라이버 외에도 [Opensqlfilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 기능을 위한 내보내기 라이브러리인 msoledbsql 라이브러리 파일이 있습니다.  
  
 SQL Server용 OLE DB 드라이버 헤더 파일은 Microsoft Data Access Components(MDAC)에서 사용되는 sqloledb.h 헤더 파일과 호환되지만 SQLOLEDB(MDAC에 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 OLE DB 공급자)에 사용되는 CLSID 또는 XML 기능(SQL Server용 OLE DB Driver에서 지원되지 않음)에 사용되는 기호는 포함하지 않습니다.    
  
 SQL Server 용 OLE DB 드라이버를 사용 하는 OLE DB 응용 프로그램은 msoledbsql를 참조 하기만 하면 됩니다. MDAC(SQLOLEDB)와 SQL Server용 OLE DB 드라이버를 모두 사용하는 애플리케이션은 sqloledb.h 및 msoledbsql.h를 모두 참조할 수 있지만 sqloledb.h를 먼저 참조해야 합니다.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>SQL Server 헤더 파일에 대 한 OLE DB 드라이버 사용  
 SQL Server 헤더 파일에 OLE DB 드라이버를 사용 하려면 C/C++ 프로그래밍 코드 내에서 **include** 문을 사용 해야 합니다. 다음 섹션에서는 OLE DB 응용 프로그램에서이 작업을 수행 하는 방법을 설명 합니다.  
  
> [!NOTE]  
>  SQL Server 헤더 및 라이브러리 파일용 OLE DB 드라이버는 Visual Studio C++ 2012 이상을 사용 해야만 컴파일할 수 있습니다.  
  
### <a name="ole-db"></a>OLE DB  
 OLE DB 응용 프로그램에서 SQL Server 헤더 파일에 대 한 OLE DB 드라이버를 사용 하려면 다음 프로그래밍 코드 행을 사용 합니다.  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  응용 프로그램에 sqloledb에 대 한 **include** 문이 있는 경우 msoledbsql에 대 한 **include** 문이 뒤에와 야 합니다.  
  
 SQL Server에 대 한 OLE DB 드라이버를 통해 데이터 원본에 대 한 연결을 만들 때 공급자 이름 문자열로 "MSOLEDBSQL"를 사용 합니다.  

  
## <a name="component-names-and-properties-by-version"></a>버전별 구성 요소 이름 및 속성  

|속성|SQL Server용 OLE DB 드라이버|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 헤더 파일 이름|msoledbsql.h|Sqloledb.h|  
|OLE DB Provider DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>정적 연결 및 BCP 함수  
 애플리케이션에서 BCP 함수를 사용하는 경우 애플리케이션의 연결 문자열에 애플리케이션을 컴파일하는 데 사용된 헤더 파일 및 라이브러리가 함께 제공되는 동일한 버전의 드라이버를 지정해야 합니다.  
  
 자세한 내용은 [대량 복사 작업](../../oledb/features/performing-bulk-copy-operations.md)수행을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
