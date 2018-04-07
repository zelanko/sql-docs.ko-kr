---
title: SQL Server 용 OLE DB 드라이버에 대 한 시스템 요구 사항 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버에 대 한 요구 사항
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5169c841784230d1ad4d99472dd636a490c750ce
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>SQL Server 용 OLE DB 드라이버에 대 한 시스템 요구 사항
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 MARS와 같은 데이터 액세스 기능을 사용하려면 다음 소프트웨어가 설치되어 있어야 합니다.  

-   OLE DB Driver for SQL Server 클라이언트에 있습니다.  

-   서버에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 설치   

> [!NOTE]  
>  이 소프트웨어를 설치하기 전에 관리자 권한으로 로그온했는지 확인하십시오.  

## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 SQL Server 용 OLE DB 드라이버를 지 원하는 운영 체제의 목록이 참조 [OLE DB Driver for SQL Server에 대 한 지원 정책을](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)합니다.  

## <a name="sql-server-requirements"></a>SQL Server 요구 사항  
 데이터에 액세스 하려면 SQL Server에 대 한 OLE DB 드라이버를 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 있어야의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SQL Server에 대 한 모든 버전의 MDAC, Windows Data Access Components 및 모든 버전의 OLE DB 드라이버에서 연결을 지원 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 이전 클라이언트 버전이 연결되어 있으면 클라이언트에서 인식되지 않는 서버 데이터 형식이 클라이언트 버전과 호환되는 형식으로 매핑됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 클라이언트 버전별 데이터 형식 호환성을 참조하십시오.  

## <a name="cross-language-requirements"></a>언어 간 상호 운용성 요구 사항  
 OLE DB Driver for SQL Server의 영어 버전은 지원 되는 운영 체제의 모든 지역화 된 버전에서 지원 됩니다. OLE DB Driver for SQL Server의 지역화 된 버전의 지역화 된 OLE DB Driver for SQL Server 버전와 같은 언어로 지역화 된 운영 체제에서 사용할 수 있습니다. OLE DB Driver for SQL Server의 지역화 된 버전으로 일치 하는 언어 설정이 설치에 지원 되는 운영 체제의 영어 버전에서 지원 됩니다.  

 업그레이드의 경우  

-   영어 버전의 OLE DB Driver for SQL Server SQL Server에 대 한 지역화 된 버전의 OLE DB 드라이버를 업그레이드할 수 있습니다.  

-   지역화 된 버전의 OLE DB Driver for SQL Server for SQL Server는 같은 언어로 지역화 된 버전의 OLE DB 드라이버를 업그레이드할 수 있습니다.  

-   지역화 된 버전의 OLE DB Driver for SQL Server SQL Server 용 OLE DB Driver의 영어 버전으로 업그레이드할 수 있습니다.  

-   지역화 된 OLE DB driver for SQL Server 버전을 다른 언어의 OLE DB Driver for SQL Server의 지역화 된 버전을 업그레이드할 수 없습니다.  

## <a name="data-type-compatibility-for-client-versions"></a>클라이언트 버전별 데이터 형식 호환성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 OLE DB Driver for SQL Server 지도 새 데이터 형식 이전 데이터와 호환 되는 하위 수준 클라이언트 아래 표에 나와 있는 것 처럼 합니다.  

 OLE DB 및 ADO 응용 프로그램에서 사용할 수는 **DataTypeCompatibility** 연결 문자열 키워드를 OLE DB Driver for SQL Server 이전 데이터 형식은 마련입니다. 때 **DataTypeCompatibility = 80**, 사용 하 여 OLE DB 클라이언트는 연결의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 테이블 형식 데이터 스트림 TDS 버전이 아닌 (TDS) 버전입니다. 에 대 한 즉 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 데이터 형식의 하위 변환이 수행 됩니다 OLE DB Driver가 아니라 서버에서 SQL Server에 대 한 합니다. 또한 연결에서 사용할 수 있는 기능이 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 기능 집합으로 제한됩니다. 새 데이터 형식이나 기능을 사용하려고 시도하면, 잘못된 요청을 서버에 전달하는 것이 아니라 API 호출에서 최대한 일찍 시도를 감지하여 호출 응용 프로그램으로 오류를 반환합니다.   


 IDBInfo::GetKeywords는 항상 영향을 받지 않는 연결에서 서버 버전에 해당 하는 키워드 목록을 반환 **DataTypeCompatibility**합니다.  

|데이터 형식|OLE DB Driver for SQL Server<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|OLE DB Driver for SQL Server|Windows Data Access Components, MDAC 및<br /><br /> OLE DB Driver for SQL Server OLE DB 응용 프로그램 datatypecompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<8kb =)|udt|Udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|텍스트|  
|nvarchar(max)|nvarchar|nvarchar|nvarchar|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|udt|varbinary|varbinary|image|  
|date|date|varchar|varchar|Varchar|  
|datetime2|datetime2|varchar|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|varchar|Varchar|  
|time|time|varchar|varchar|Varchar|  

## <a name="see-also"></a>관련 항목:  
 [SQL Server 프로그래밍에 대 한 OLE DB 드라이버](../oledb/oledb-driver-for-sql-server-programming.md)   
 [SQL Server용 OLE DB 드라이버 설치](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
