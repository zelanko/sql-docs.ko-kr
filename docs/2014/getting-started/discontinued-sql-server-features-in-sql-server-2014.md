---
title: SQL Server 2014의 지원 되지 않는 SQL Server 기능 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 0678bfbc-5d3f-44f4-89c0-13e8e52404da
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8f7ab6cdbc1b6e0e3dc7d26fb579943a0c8fa95
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637779"
---
# <a name="discontinued-sql-server-features-in-sql-server-2014"></a>SQL Server 2014에서 지원되지 않는 SQL Server 기능
  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 업그레이드한 후 더 이상 사용할 수 없는 기능에 대해 설명합니다.  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에서는 지원되지 않는 기능이 없습니다.  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="discontinued-active-directory-helper-service"></a>지원되지 않는 Active Directory Helper 서비스  
 Active Directory Helper 서비스 및 관련 구성 요소가 제거되었습니다. 다음 표에서는 이와 관련하여 제거된 구성 요소를 보여 줍니다.  
  
|범주|지원되지 않는 기능|대체 기능|  
|--------------|--------------------------|-----------------|  
|시스템 저장 프로시저|sp_ActiveDirectory_Obj<br /><br /> sp_ActiveDirectory_SCP<br /><br /> sp_ActiveDirectory_Start|사용 가능한 대체 항목 없음|  
  
## <a name="discontinued-features-in-sql-server-2008-r2"></a>SQL Server 2008 R2에서 지원되지 않는 기능  
  
### <a name="64-bit-platform-support-in-reporting-services"></a>Reporting Services의 64비트 플랫폼 지원  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]부터 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 요소는 더 이상 Windows Server 2003 또는 Windows Server 2003 R2를 실행하는 Itanium 기반 서버를 지원하지 않습니다. Itanium 기반 시스템용 Windows Server°2008 및 Itanium 기반 시스템용 Windows Server°2008°R2를 포함하여 기타 64비트 운영 체제는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 계속 지원합니다. Itanium 기반 시스템 버전의 Windows Server 2003 또는 Windows Server 2003 R2에서 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 를 포함하는 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 설치를 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 로 업그레이드하려면 먼저 운영 체제를 업그레이드해야 합니다.  
  
## <a name="discontinued-features-in-sql-server-2008"></a>SQL Server 2008에서 지원되지 않는 기능  
  
### <a name="discontinued-sql-dmo-from-sql-server-express-installation"></a>SQL Server Express 설치에서 더 이상 제공되지 않는 SQL-DMO  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]용 SQL-DMO가 [!INCLUDE[ssExpressEd10](../includes/ssexpressed10-md.md)]에서 제거되었습니다. 현재 이 기능을 사용하는 애플리케이션을 가능한 한 빨리 수정하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 용 sql-dmo를 지원 해야 하는 경우 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=24793)에서 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 기능 팩의 이전 버전과의 호환성 구성 요소를 설치 합니다. 새로운 개발 작업에는 SMO([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects)를 사용하십시오.  
  
### <a name="discontinued-option-for-web-assistant"></a>더 이상 제공되지 않는 웹 길잡이 옵션  
 웹 길잡이를 사용할 수 있도록 설정하는 `sp_configure` 옵션이 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서 제거되었습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 를 사용하는 것이 좋습니다.  
  
### <a name="surface-area-configuration-tool"></a>노출 영역 구성 도구  
 노출 영역 구성 도구는 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서 더 이상 사용되지 않습니다. 다음 표에서는 이 릴리스의 설정, 옵션 및 구성 요소 기능을 구성하는 데 사용할 수 있는 내용을 보여 줍니다.  
  
|대체 설정 및 구성 요소 기능|구성 방법|  
|-------------------------------------------------|----------------------|  
|프로토콜, 연결 및 시작 옵션|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용합니다.|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] 기능|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 속성 설정을 사용하거나 sp_Configure를 사용합니다.|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 기능|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 속성 설정을 사용합니다.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-EnableIntegrated 보안 속성|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 속성 설정을 사용합니다.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-"예약 이벤트 및 보고서 배달" 및 "웹 서비스 및 HTTP 액세스"|RSReportServer.config 구성 파일을 편집합니다.|  
|명령줄 옵션|이 릴리스에서 지원되지 않습니다.|  
|SOAP 및 [!INCLUDE[ssSB](../includes/sssb-md.md)] 엔드포인트|[CREATE endpoint](/sql/t-sql/statements/create-endpoint-transact-sql)및 [ALTER endpoint](/sql/t-sql/statements/alter-endpoint-transact-sql)를 사용 합니다.|  
  
### <a name="discontinued-command-prompt-parameters-for-sql-server-setup"></a>SQL Server 설치에 지원되지 않는 명령 프롬프트 매개 변수  
 다음 표에서는 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 지원되지만 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 지원되지 않는 설치 명령 프롬프트 매개 변수를 보여 줍니다.  
  
|지원되지 않는 매개 변수|대체 매개 변수|  
|----------------------------|---------------------------|  
|ADDLOCAL|/ACTION=Uninstall 및 /FEATURES|  
|DISABLENETWORKPROTOCOLS|Tcp/ip가 tcp/ip<sup>1</sup> 에 대해 사용 하도록 설정 됨|  
|DISABLENETWORKPROTOCOLS|명명 된 파이프<sup>1</sup> 에 대해/NPENABLED|  
|INSTALLSQLDATADIR|/SQLUSERDBDIR<br /><br /> /SQLUSERDBLOGDIR<br /><br /> /SQLBACKUPDIR<br /><br /> /SQLTEMPDBDIR<br /><br /> /SQLTEMPDBLOGDIR|  
|REINSTALL|이 릴리스에는 해당 항목이 없습니다.|  
|REINSTALLMODE|이 릴리스에는 해당 항목이 없습니다.|  
|REMOVE|/ACTION=Uninstall 및 /FEATURES|  
|SAMPLEDATABASE|이 릴리스에는 해당 항목이 없습니다.|  
|SAVESYSDB|이 릴리스에는 해당 항목이 없습니다.|  
|이상 업그레이드<sup>2</sup>|이 릴리스에는 해당 항목이 없습니다.|  
|UPGRADE|/ACTION=Upgrade 및 /FEATURES|  
|USESYSDB|이 릴리스에는 해당 항목이 없습니다.|  
  
 <sup>1</sup> 이러한 매개 변수는 설치에만 유효 합니다.  
  
 <sup>2</sup> 원래 설치 미디어를 사용 하지 않고 언제 든 지/Action = EditionUpgrade을 지정 하 여 기존 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 다른 버전으로 업그레이드 합니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 지원되는 버전 및 버전 업그레이드에 대한 자세한 내용은 [Supported Version and Edition Upgrades](../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하십시오.  
  
 자세한 내용은 [명령 프롬프트에서 SQL Server 2014 설치](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조하세요.  
  
  
