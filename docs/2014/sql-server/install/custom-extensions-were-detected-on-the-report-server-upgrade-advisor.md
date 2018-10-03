---
title: 사용자 지정 확장 프로그램이 보고서 서버 (업그레이드 관리자)에서 검색 됨 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- rendering extensions [Reporting Services], custom extensions
- security extensions [Reporting Services]
- custom extensions [Reporting Services]
- data processing extensions [Reporting Services], custom extensions
- delivery extensions [Reporting Services]
ms.assetid: fa184bd7-11d6-4ea3-9249-bc1b13db49e5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 86c0aa75e73c59980e8de6456556087201d949d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153103"
---
# <a name="custom-extensions-were-detected-on-the-report-server-upgrade-advisor"></a>보고서 서버에서 사용자 지정 확장 프로그램이 검색됨(업그레이드 관리자)
  업그레이드 관리자가 구성 파일에서 사용자 지정 확장 프로그램 설정을 검색했으며, 이는 데이터 처리, 배달, 렌더링, 보안 또는 인증을 위한 하나 이상의 사용자 지정 확장이 사용자 설치에 포함되어 있음을 나타냅니다. 업그레이드 관리자는 업그레이드된 보고서 서버와 함께 확장 프로그램 구성 설정을 이동합니다. 그러나 사용자 지정 확장 프로그램이 기존 보고서 서버 설치 폴더에 설치되어 있으면 업그레이드 프로세스 중 해당 사용자 지정 확장 프로그램에 대한 어셈블리 파일이 새 설치 폴더로 이동되지 않습니다. 이 경우 업그레이드가 완료된 후 어셈블리 파일을 새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 폴더로 이동해야 합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개발자가 데이터 처리, 배달, 렌더링, 보안 및 인증에 대 한 사용자 지정 확장 프로그램을 만들 수 있도록 확장 가능한 아키텍처를 제공 합니다.  
  
 사용자 지정 확장 프로그램 또는 어셈블리가 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치에서 사용되는 경우 설치 프로그램을 사용하여 업그레이드를 수행할 수 있지만 업그레이드가 완료된 후 확장 프로그램을 새 설치 위치로 이동하거나 업그레이드 전 단계를 수행해야 합니다.  
  
> [!NOTE]  
>  업그레이드 관리자는 사용자 지정 코드 어셈블리가 보고서에서 항목 값, 스타일 및 서식을 계산할 용도로 사용되도록 구성되어 있는지 여부를 감지하지 못합니다. 자세한 내용은 [기타 Reporting Services 업그레이드 문제](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)합니다.  
  
 소프트웨어 공급업체로부터 사용자 지정 확장 프로그램을 구입한 경우 해당 업체에 사용자 지정 기능의 업그레이드에 대한 추가 정보를 문의하십시오.  
  
## <a name="corrective-action"></a>수정 동작  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 업그레이드하기 전이나 후에 수행할 단계를 확인하려면 다음 섹션을 참조하십시오.  
  
 [사용자 지정 데이터 처리 또는 배달 확장 프로그램](#dataprocdeliver)  
  
 [사용자 지정 렌더링 확장 프로그램](#render)  
  
 [SQL Server 2000 보고서 서버에서 사용자 지정 보안 또는 인증 확장 프로그램](#secauth2000)  
  
 [SQL Server 2005 보고서 서버에서 사용자 지정 보안 또는 인증 확장 프로그램](#secauth2005)  
  
 업그레이드가 완료된 후 확장 프로그램 어셈블리를 새 설치 폴더로 이동한 다음 사용자 지정 확장 프로그램이 예상대로 작동하는지 확인합니다. 확장 프로그램이 작동하지 않으면 다음과 같이 다시 컴파일합니다.  
  
#### <a name="to-recompile-an-extension"></a>확장 프로그램을 다시 컴파일하려면  
  
1.  Microsoft.ReportingServices.Interfaces.dll 파일을 원본 코드가 포함된 폴더에 복사합니다.  
  
2.  원본 파일이 포함된 프로젝트를 열고 Microsoft.ReportingServices.Interfaces.dll 파일에 대한 참조를 추가합니다.  
  
3.  솔루션을 다시 빌드하여 확장 프로그램을 바인딩합니다.  
  
 업그레이드를 중단하려는 경우 대신 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 마이그레이션하는 방법을 고려해 볼 수 있습니다. 사용자 지정 확장 프로그램을 마이그레이션하는 단계를 참조 하세요 [사용자 지정 확장 프로그램 마이그레이션](#migrcustext) 이 항목의 합니다.  
  
###  <a name="dataprocdeliver"></a> 사용자 지정 데이터 처리 또는 배달 확장 프로그램  
 업그레이드 관리자가 사용자 지정 데이터 처리 또는 배달 확장 프로그램을 검색할 경우 업그레이드 프로세스가 차단되지 않습니다. 그러나 업그레이드가 완료된 후 추가 단계를 수행해야만 이러한 확장 프로그램에서 제공하는 사용자 지정 기능이 작동합니다. 예를 들어 사용자 지정 확장 프로그램 파일이 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 폴더에 설치되어 있으면 업그레이드가 완료된 후 추가 단계를 수행해야 합니다.  
  
##### <a name="post-upgrade-steps-for-custom-data-processing-or-delivery-extensions"></a>사용자 지정 데이터 처리 또는 배달 확장 프로그램에 대해 수행할 업그레이드 후 단계  
  
1.  확장 프로그램 파일을 새 보고서 서버 프로그램 폴더로 이동합니다. 기본적으로 보고서 서버 프로그램 폴더 \Program Files\Microsoft SQL Server\MSRS10_50에 있습니다. \< *instance_name*> \report server입니다.  
  
 자세한 내용은 SQL Server 온라인 설명서의 "데이터 처리 확장 프로그램 배포" 및 "배달 확장 프로그램 구현"을 참조하십시오.  
  
###  <a name="render"></a> 사용자 지정 렌더링 확장 프로그램  
 업그레이드 관리자가 사용자 지정 렌더링 확장 프로그램을 검색할 경우 업그레이드 프로세스가 차단됩니다. 구성 파일에서 사용자 지정 확장 프로그램 구성 항목을 제거하여 업그레이드 프로세스를 계속할 수 있습니다. 그러나 이렇게 하면 업그레이드가 완료된 후 사용자 지정 확장 프로그램을 사용할 수 없게 됩니다. 업그레이드 후 사용자 지정 렌더링 확장 프로그램이 필요한 경우 업데이트된 렌더링 확장 프로그램을 만들거나 사용자 지정 확장 프로그램 공급업체에서 업데이트된 렌더링 확장 프로그램을 구해야 합니다.  
  
 업그레이드 지원을 위한 단계를 수행해야 하거나 대신 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 마이그레이션할 수도 있습니다.  
  
> [!IMPORTANT]  
>  업데이트된 렌더링 확장 프로그램이 예상대로 작동하는지 테스트하고 확인하기 전까지는 보고서 서버를 업그레이드하거나 마이그레이션하지 마십시오.  
  
##### <a name="to-upgrade-custom-rendering-extensions"></a>사용자 지정 렌더링 확장 프로그램을 업그레이드하려면  
  
1.  최신 인터페이스가 있는 렌더링 확장 프로그램을 구합니다.  
  
2.  RSReportServer.config에서 이전 사용자 지정 렌더링 확장 프로그램 항목을 제거합니다.  
  
3.  보고서 서버를 업그레이드합니다.  
  
4.  업그레이드가 완료된 후 업데이트된 확장 프로그램을 보고서 서버에 설치합니다.  
  
 자세한 내용은 SQL Server 온라인 설명서의 "렌더링 확장 프로그램 구현"을 참조하십시오.  
  
###  <a name="secauth2000"></a> SQL Server 2000 보고서 서버에서 사용자 지정 보안 또는 인증 확장 프로그램  
 업그레이드 관리자가 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 보고서 서버에서 사용자 지정 보안 또는 인증 확장 프로그램을 검색할 경우 업그레이드 프로세스가 차단됩니다. 업그레이드 지원을 위한 단계를 수행해야 하거나 대신 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 마이그레이션할 수도 있습니다. [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]로 넘어오면서 인터페이스가 변경되었기 때문에 어떤 방법을 선택하든 Microsoft.ReportingServices.Interfaces.dll의 최신 인터페이스로 확장 프로그램을 업데이트하고 다시 컴파일해야 합니다.  
  
> [!IMPORTANT]  
>  업데이트된 보안 또는 인증 확장 프로그램이 예상대로 작동하는지 테스트하고 확인하기 전까지는 보고서 서버를 업그레이드하거나 마이그레이션하지 마십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]용으로 작성한 사용자 지정 인증 확장 프로그램을 사용 중인 경우 모델 기반 보고를 위해 새로 도입된 새 클래스와 멤버를 지원하도록 원본 코드를 수정해야 합니다.  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2000-report-server"></a>SQL Server 2000 보고서 서버에서 사용자 지정 보안 또는 인증 확장 프로그램을 업그레이드 하려면  
  
1.  보안 또는 인증 확장 프로그램을 최신 인터페이스로 업데이트하고 다시 컴파일합니다.  
  
2.  RSReportServer.config에서 보안 또는 인증 확장 프로그램 항목을 제거합니다.  
  
3.  보고서 서버를 업그레이드합니다.  
  
4.  업그레이드가 완료된 후 업데이트된 확장 프로그램을 보고서 서버에 설치합니다.  
  
 자세한 내용은 SQL Server 온라인 설명서의 "보안 확장 프로그램 구현"을 참조하십시오.  
  
###  <a name="secauth2005"></a> SQL Server 2005 보고서 서버에서 사용자 지정 보안 또는 인증 확장 프로그램  
 업그레이드 관리자가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 보고서 서버에서 사용자 지정 보안 또는 인증 확장 프로그램을 검색할 경우 업그레이드 프로세스가 차단됩니다. 업그레이드 지원을 위한 단계를 수행해야 하거나 대신 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 마이그레이션할 수도 있습니다.  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2005-report-server"></a>SQL Server 2005 보고서 서버의 사용자 지정 보안 또는 인증 확장 프로그램을 업그레이드하려면  
  
1.  RSReportServer.config에서 보안 또는 인증 확장 프로그램 구성 항목을 제거합니다.  
  
2.  보고서 서버를 업그레이드합니다.  
  
3.  업그레이드가 완료된 후 구성 항목을 RSReportServer.config에 다시 추가합니다.  
  
4.  확장 프로그램 어셈블리가 이전 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 폴더에 설치되어 있으면 새 설치 폴더로 이동합니다.  
  
 자세한 내용은 SQL Server 온라인 설명서의 "보안 확장 프로그램 구현"을 참조하십시오.  
  
###  <a name="migrcustext"></a> 사용자 지정 확장 프로그램 마이그레이션  
 업그레이드를 수행하는 대신 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 마이그레이션하려는 경우 다음 단계를 수행하여 사용자 지정 확장 프로그램을 새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스로 마이그레이션합니다.  
  
##### <a name="to-migrate-custom-extensions-to-a-new-reporting-services-instance"></a>사용자 지정 확장 프로그램을 새 Reporting Services 인스턴스로 마이그레이션하려면  
  
1.  최신 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인터페이스가 있는 업데이트된 확장 프로그램을 만들거나 구합니다.  
  
2.  보고서 서버를 새 인스턴스로 마이그레이션합니다.  
  
3.  새 인스턴스에서 확장 프로그램을 구성합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
