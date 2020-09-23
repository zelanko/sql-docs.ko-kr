---
title: SQL Server용 OLE DB 드라이버의 시스템 요구 사항
description: OLE DB Driver for SQL Server의 MARS와 같이 SQL Server의 데이터 액세스 기능을 사용하는 데 필요한 소프트웨어 필수 구성 요소에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c86f62f98e81ce3c4fdd86e1e79e8f73e1422851
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861814"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버의 시스템 요구 사항

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 MARS와 같은 데이터 액세스 기능을 사용하려면 다음 소프트웨어가 설치되어 있어야 합니다.  

* 클라이언트에 OLE DB Driver for SQL Server.  
* 서버에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 설치

> [!NOTE]  
> 이 소프트웨어를 설치하기 전에 관리자 권한으로 로그온했는지 확인하십시오.  

## <a name="operating-system-requirements"></a>운영 체제 요구 사항  

OLE DB Driver for SQL Server를 지원하는 운영 체제 목록은 [OLE DB Driver for SQL Server에 대한 지원 정책](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)을 참조하세요.  

## <a name="azure-active-directory-authentication-requirements"></a>Azure Active Directory 인증 요구 사항  

18.3 이전 버전의 OLE DB Driver for SQL Server 버전에서 Azure Active Directory 인증 방법을 사용하는 경우 [SQL Server용 Active Directory 인증 라이브러리](https://go.microsoft.com/fwlink/?LinkID=513072)가 설치되었는지 확인합니다.****** (버전 18.3에는 설치 프로그램 패키지의 일부로 종속성이 포함되어 있습니다.) ADAL은 다른 인증 방법 또는 OLE DB 작업에 필요하지 않습니다. 자세한 내용은 다음을 참조하세요. [Azure Active Directory 사용](features/using-azure-active-directory.md).

## <a name="sql-server-requirements"></a>SQL Server 요구 사항  

OLE DB Driver for SQL Server를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터에 액세스하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 설치되어 있어야 합니다.  

[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]은 모든 버전의 MDAC, Windows Data Access Components 및 모든 버전의 SQL Server용 OLE DB 드라이버에서 연결을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 이전 클라이언트 버전이 연결되어 있으면 클라이언트에서 인식되지 않는 서버 데이터 형식이 클라이언트 버전과 호환되는 형식으로 매핑됩니다. 자세한 내용은 [클라이언트 버전별 데이터 형식 호환성](#data-type-compatibility-for-client-versions)을 참조하세요.  

## <a name="cross-language-requirements"></a>언어 간 상호 운용성 요구 사항  

영어 버전의 OLE DB Driver for SQL Server는 모든 언어 버전의 지원 운영 체제에서 지원됩니다. 지역화 버전의 OLE DB Driver for SQL Server는 OLE DB Driver for SQL Server 지역화 언어와 같은 언어로 지역화된 운영 체제에서 지원됩니다. 각 언어 버전의 SQL Server용 OLE DB 드라이버는 언어 설정이 일치하는 경우 영어 버전의 지원 운영 체제에서도 지원됩니다.  

업그레이드의 경우  

* 영어 버전의 OLE DB Driver for SQL Server는 모든 지역화 버전의 OLE DB Driver for SQL Server로 업그레이드할 수 있습니다.  
* 지역화 버전의 OLE DB Driver for SQL Server는 동일한 언어로 지역화된 OLE DB Driver for SQL Server로 업그레이드할 수 있습니다.  
* 지역화 버전의 OLE DB Driver for SQL Server는 영어 버전의 OLE DB Driver for SQL Server로 업그레이드할 수 있습니다.  
* 지역화 버전의 OLE DB Driver for SQL Server는 언어가 다른 지역화 버전의 OLE DB Driver for SQL Server로 업그레이드할 수 없습니다.  

## <a name="data-type-compatibility-for-client-versions"></a>클라이언트 버전별 데이터 형식 호환성  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 SQL Server용 OLE DB 드라이버는 아래 표에서와 같이 새 데이터 형식을 하위 클라이언트와 호환되는 이전 데이터 형식으로 매핑합니다.  

OLE DB 및 ADO 애플리케이션은 OLE DB Driver for SQL Server에 **DataTypeCompatibility** 연결 문자열 키워드를 사용하여 이전 데이터 형식으로 작동할 수 있습니다. **DataTypeCompatibility=80**이면 OLE DB 클라이언트는 TDS 버전이 아닌, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] TDS(Tabular Data Stream) 버전을 사용하여 연결합니다. 이는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 데이터 형식의 경우 SQL Server용 OLE DB 드라이버가 아닌 서버에 의해 하위 변환이 수행된다는 의미입니다. 또한 연결에서 사용할 수 있는 기능이 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 기능 집합으로 제한됩니다. 새 데이터 형식이나 기능을 사용하려고 시도하면, 잘못된 요청을 서버에 전달하는 것이 아니라 API 호출에서 최대한 일찍 시도를 감지하여 호출 애플리케이션으로 오류를 반환합니다.  

IDBInfo::GetKeywords는 항상 연결의 서버 버전에 해당하는 키워드 목록을 반환하고 **DataTypeCompatibility**의 영향을 받지 않습니다.  

|데이터 형식|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SQL Server용 OLE DB 드라이버|Windows Data Access Components, MDAC 및<br /><br /> OLE DB Driver for SQL Server OLE DB 애플리케이션(DataTypeCompatibility=80)|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT(\<= 8Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|이미지|  
|varchar(max)|varchar|varchar|varchar|텍스트|  
|nvarchar(max)|nvarchar|nvarchar|nvarchar|Ntext|  
|Xml|Xml|Xml|Xml|Ntext|  
|CLR UDT(> 8Kb)|varbinary|udt|udt|이미지|  
|date|varchar|date|date|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>참고 항목  

[SQL Server용 OLE DB 드라이버](../oledb/oledb-driver-for-sql-server.md)  
[SQL Server용 OLE DB 드라이버 설치](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
