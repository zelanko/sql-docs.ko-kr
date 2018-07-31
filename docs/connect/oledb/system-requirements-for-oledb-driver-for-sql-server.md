---
title: SQL Server용 OLE DB 드라이버의 시스템 요구 사항 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버의 시스템 요구 사항
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d7b390f385f94dbe65d667440d27e748a84bcb86
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106579"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버의 시스템 요구 사항
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 MARS와 같은 데이터 액세스 기능을 사용하려면 다음 소프트웨어가 설치되어 있어야 합니다.  

-   OLE DB Driver for SQL Server 클라이언트입니다.  

-   서버에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 설치   

> [!NOTE]  
>  이 소프트웨어를 설치하기 전에 관리자 권한으로 로그온했는지 확인하십시오.  

## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 SQL Server에 대 한 OLE DB 드라이버를 지 원하는 운영 체제 목록은 참조 하세요 [OLE DB Driver for SQL Server에 대 한 지원 정책을](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)합니다.  

## <a name="sql-server-requirements"></a>SQL Server 요구 사항  
 SQL Server 용 OLE DB 드라이버를 사용 하 여 데이터에 액세스 하도록 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 인스턴스에 있어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]은 모든 버전의 MDAC, Windows Data Access Components 및 모든 버전의 SQL Server용 OLE DB 드라이버에서 연결을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 이전 클라이언트 버전이 연결되어 있으면 클라이언트에서 인식되지 않는 서버 데이터 형식이 클라이언트 버전과 호환되는 형식으로 매핑됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 클라이언트 버전별 데이터 형식 호환성을 참조하십시오.  

## <a name="cross-language-requirements"></a>언어 간 상호 운용성 요구 사항  
 OLE DB Driver for SQL Server의 영어 버전은 지원 되는 운영 체제의 모든 지역화 된 버전에서 지원 됩니다. OLE DB Driver for SQL Server의 지역화 된 버전의 지역화 된 OLE DB 드라이버로 SQL Server 버전에 대 한 동일한 언어로 지역화 된 운영 체제에서 지원 됩니다. 각 언어 버전의 SQL Server용 OLE DB 드라이버는 언어 설정이 일치하는 경우 영어 버전의 지원 운영 체제에서도 지원됩니다.  

 업그레이드의 경우  

-   영어 버전 OLE DB Driver for SQL Server의 SQL Server 용 OLE DB 드라이버의 지역화 된 버전으로 업그레이드할 수 있습니다.  

-   OLE DB Driver for SQL Server의 지역화 된 버전은 동일한 언어의 SQL Server에 대 한 지역화 된 버전의 OLE DB 드라이버를 업그레이드할 수 있습니다.  

-   지역화 된 버전 OLE DB Driver for SQL Server의 SQL Server 용 OLE DB 드라이버의 영어 버전으로 업그레이드할 수 있습니다.  

-   지역화 된 OLE DB 드라이버에는 다른 언어의 SQL Server 버전에 대 한 지역화 된 버전의 OLE DB Driver for SQL Server를 업그레이드할 수 없습니다.  

## <a name="data-type-compatibility-for-client-versions"></a>클라이언트 버전별 데이터 형식 호환성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 SQL Server용 OLE DB 드라이버는 아래 표에서와 같이 새 데이터 형식을 하위 클라이언트와 호환되는 이전 데이터 형식으로 매핑합니다.  

 OLE DB 및 ADO 응용 프로그램에서 사용할 수는 **DataTypeCompatibility** OLE DB 드라이버 이전 데이터 형식은 함께 작동 하도록 SQL Server에 대 한 연결 문자열 키워드입니다. **DataTypeCompatibility=80**이면 OLE DB 클라이언트는 TDS 버전이 아닌, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] TDS(Tabular Data Stream) 버전을 사용하여 연결합니다. 이는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 데이터 형식의 경우 SQL Server용 OLE DB 드라이버가 아닌 서버에 의해 하위 변환이 수행된다는 의미입니다. 또한 연결에서 사용할 수 있는 기능이 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 기능 집합으로 제한됩니다. 새 데이터 형식이나 기능을 사용하려고 시도하면, 잘못된 요청을 서버에 전달하는 것이 아니라 API 호출에서 최대한 일찍 시도를 감지하여 호출 응용 프로그램으로 오류를 반환합니다.   


 IDBInfo::GetKeywords는 항상 해당 서버 버전에 연결 하 고 영향을 받지는 키워드 목록을 반환 **DataTypeCompatibility**합니다.  

|데이터 형식|SQL Server Native Client <br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SQL Server용 OLE DB 드라이버|Windows Data Access Components, MDAC 및<br /><br /> OLE DB 드라이버 응용 프로그램의 SQL Server OLE DB DataTypeCompatibility 사용 하 여 = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT(\<= 8Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|텍스트 모드|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|varbinary|udt|udt|image|  
|날짜|varchar|날짜|날짜|Varchar|  
|Datetime2|varchar|Datetime2|Datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|Time|varchar|Time|Time|Varchar|  

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버](../oledb/oledb-driver-for-sql-server.md)   
 [SQL Server용 OLE DB 드라이버 설치](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
