---
title: SQL Server Native Client에 대 한 시스템 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [SQL Server Native Client]
- data access [SQL Server Native Client], system requirements
- SQL Server Native Client, system requirements
- SQLNCLI, system requirements
ms.assetid: 1c8e2f8a-a440-44da-8e3a-af632d34c52c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85b00f00e2c557f31a7343a99e1f2592741a6b59
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637792"
---
# <a name="system-requirements-for-sql-server-native-client"></a>SQL Server Native Client의 시스템 요구 사항
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 MARS와 같은 데이터 액세스 기능을 사용하려면 다음 소프트웨어가 설치되어 있어야 합니다.  
  
-   클라이언트에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 설치  
  
-   서버에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 설치  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에는 Windows Installer 3.0이 필요합니다. Windows Installer 3.0은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 운영 체제에는 기본적으로 설치되어 있으며, 그 외의 다른 플랫폼에는 이를 명시적으로 설치해야 합니다. 자세한 내용은 [Windows Installer 3.0 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=16821)를 참조 하세요.  
  
> [!NOTE]  
>  이 소프트웨어를 설치하기 전에 관리자 권한으로 로그온했는지 확인하십시오.  
  
## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 지 원하는 운영 체제 목록은 [SQL Server Native Client에 대 한 지원 정책](applications/support-policies-for-sql-server-native-client.md)을 참조 하세요.  
  
## <a name="sql-server-requirements"></a>SQL Server 요구 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터에 액세스하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 설치되어 있어야 합니다.  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]은 모든 버전의 MDAC, Windows Data Access Components 및 모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 연결을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 이전 클라이언트 버전이 연결되어 있으면 클라이언트에서 인식되지 않는 서버 데이터 형식이 클라이언트 버전과 호환되는 형식으로 매핑됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 클라이언트 버전별 데이터 형식 호환성을 참조하십시오.  
  
## <a name="cross-language-requirements"></a>언어 간 상호 운용성 요구 사항  
 영어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 모든 언어 버전의 지원 운영 체제에서 지원됩니다. 각 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 해당 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 같은 언어로 지역화된 운영 체제에서 지원됩니다. 각 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 언어 설정이 일치하는 경우 영어 버전의 지원 운영 체제에서도 지원됩니다.  
  
 업그레이드의 경우  
  
-   영어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 모든 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client로 업그레이드할 수 있습니다.  
  
-   각 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 같은 언어로 지역화된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 버전으로 업그레이드할 수 있습니다.  
  
-   각 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 영어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client로 업그레이드할 수 있습니다.  
  
-   각 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 다른 언어로 지역화된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 버전으로 업그레이드할 수 없습니다.  
  
## <a name="data-type-compatibility-for-client-versions"></a>클라이언트 버전별 데이터 형식 호환성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 아래 표에서와 같이 새 데이터 형식을 하위 클라이언트와 호환되는 이전 데이터 형식으로 매핑합니다.  
  
 OLE DB 및 ADO 애플리케이션은 `DataTypeCompatibility` 연결 문자열 키워드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 이전 데이터 형식이 작동되도록 합니다. `DataTypeCompatibility=80`이면 OLE DB 클라이언트는 TDS 버전이 아닌, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] TDS(Tabular Data Stream) 버전을 사용하여 연결합니다. 이는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 데이터 형식의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 아닌 서버에 의해 하위 변환이 수행된다는 의미입니다. 또한 연결에서 사용할 수 있는 기능이 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 기능 집합으로 제한됩니다. 새 데이터 형식이나 기능을 사용하려고 시도하면, 잘못된 요청을 서버에 전달하는 것이 아니라 API 호출에서 최대한 일찍 시도를 감지하여 호출 애플리케이션으로 오류를 반환합니다.  
  
 ODBC에는 `DataTypeCompatibility` 컨트롤이 없습니다.  
  
 IDBInfo:: GetKeywords는 항상 연결의 서버 버전에 해당 하는 키워드 목록을 반환 하며 `DataTypeCompatibility`의 영향을 받지 않습니다.  
  
|데이터 형식|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Windows Data Access Components, MDAC 및<br /><br /> SQL Server Native Client OLE DB 애플리케이션에서 DataTypeCompatibility=80 설정|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT(\<= 8Kb)|udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|이미지|  
|varchar(max)|varchar|varchar|텍스트|  
|nvarchar(max)|nvarchar|nvarchar|Ntext|  
|XML|XML|XML|Ntext|  
|CLR UDT (> 8Kb)|udt|varbinary|이미지|  
|date|date|varchar|Varchar|  
|datetime2|datetime2|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|Varchar|  
|time|time|varchar|Varchar|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 프로그래밍](sql-server-native-client-programming.md)   
 [SQL Server Native Client 설치](applications/installing-sql-server-native-client.md)  
  
  
