---
title: 보고서 서버 상태 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serverstatus.F1
ms.assetid: 2f63ad1c-1bc2-449d-b451-fb39a0060838
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 217fc6d3d5a94fb443ea262563255c10bcfc2dda
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057959"
---
# <a name="report-server-status-ssrs-native-mode"></a>보고서 서버 상태(SSRS 기본 모드)
  이 페이지를 사용하여 현재 연결된 보고서 서버 인스턴스에 대한 정보를 볼 수 있습니다. 이 페이지는 보고서 서버 구성의 시작 페이지입니다. 추가 페이지에서는 URL, 서비스 계정, 보고서 서버 데이터베이스, 보고서 서버 전자 메일 배달, 스케일 아웃 배포 및 암호화 키를 구성할 수 있습니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작한 후 보고서 서버 인스턴스에 연결합니다. 자세한 내용은 [Reporting Services 구성 관리자 &#40;del&#41;](reporting-services-configuration-manager-native-mode.md)합니다.  
  
> [!TIP]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자 (RSConfigTool.exe)는 "highestAvailable"의 권한 수준으로 설치 됩니다. 이 동작은 의도된 것입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI API와의 통신이 필요합니다. 일부 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 통신에는 더 높은 수준 또는 관리자 권한이 필요합니다.  
  
 보고서 서버에 연결하면 모든 페이지 링크가 회색으로 표시될 경우 보고서 서버 서비스가 시작되었는지 확인합니다. **서비스 상태를 보고 합니다.** "시작" 이어야 합니다. 관리자 도구의 서비스 콘솔 애플리케이션을 사용하여 서비스 상태를 확인할 수도 있습니다.  
  
## <a name="options"></a>변수  
 **SQL Server 인스턴스**  
 현재 연결 중인 보고서 서버 인스턴스에 대한 정보를 표시합니다. 보고서 서버 인스턴스 이름은 명명된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 기반으로 합니다. 기본 인스턴스는 MSSQLSERVER입니다. 명명된 인스턴스는 사용자가 설치 중 지정한 값입니다. 인스턴스에 대 한 자세한 내용은 참조 하세요. [여러 버전 및 SQL Server 인스턴스 작업](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md) 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
> [!NOTE]  
>  SQL Server Express with Advanced Services에서 기본 인스턴스는 SQLExpress입니다.  
  
 **인스턴스 ID**  
 연결한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 프로그램 파일을 저장하는 파일 시스템의 폴더에 해당합니다. **Instance ID** 값은 설치 프로그램에 의해 *component*.*instance*형식으로 지정됩니다. 여기서 *component* 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 나타내는 값이고 *instance* 는 인스턴스 이름입니다. 기본 인스턴스 이름은 MSSQLSERVER입니다. 예를 들어 [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 기본 인스턴스를 설치할 경우 해당 폴더 이름은 다음과 같습니다.  
  
-   MSSQL12.MSSQLSERVER  
  
-   MSAS12.MSSQLSERVER  
  
-   MSRS12.MSSQLSERVER  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]과 같은 이미 설치된 구성 요소의 두 번째 인스턴스를 설치하고 이 인스턴스 이름을 Contoso로 지정할 경우 **인스턴스 ID** 는 MSSQL12.Contoso입니다.  
  
 **버전(Edition)**  
 버전 정보를 표시합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 버전에서 지원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)을 참조하세요.  
  
 **제품 버전**  
 설치한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전을 표시합니다.  
  
 **보고서 서버 데이터베이스**  
 현재 보고서 서버 인스턴스에 대한 애플리케이션 데이터를 저장하는 보고서 서버 데이터베이스의 이름을 표시합니다.  
  
 **보고서 서버 모드**  
 항상 **기본**을 값으로 표시해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 기본 모드 보고서 서버만 지원합니다. 값이 **SharePoint 통합 모드**로 표시된 경우 기본 모드 배포가 올바르게 구성되지 않아서 기본 모드 보고서 카탈로그에 연결해야 함을 나타낼 수 있습니다. 구성 관리자의 **데이터베이스** 페이지를 사용하여 데이터베이스를 변경하고 새 데이터베이스를 만들거나 기존 기본 모드 보고서 서버의 데이터베이스 카탈로그에 연결합니다.  
  
 **서버 상태**  
 보고서 서버 서비스가 실행 중인지 여부를 표시합니다.  
  
 **시작**  
 보고서 서버 서비스를 시작합니다. 컴퓨터 이름을 변경한 후에 보고서 서버를 다시 구성하는 경우처럼 일부 구성을 변경한 후에는 서비스를 다시 시작해야 합니다. URL 예약을 다시 구성하면 서비스가 자동으로 다시 시작됩니다. 변경을 적용하려면 다시 시작해야 합니다.  
  
 **중지**  
 보고서 서버 서비스를 중지합니다. 서비스를 중지하면 보고서 서버의 작동이 중지됩니다. 자세한 내용은 [보고서 서버 서비스 시작 및 중지](../../reporting-services/report-server/start-and-stop-the-report-server-service.md) 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services 구성 관리자 &#40;del&#41;](/sql/2014/sql-server/install/reporting-services-configuration-manager-native-mode)   
 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
