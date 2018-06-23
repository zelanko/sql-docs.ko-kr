---
title: 데이터베이스 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.rsconfigtool.databasesetup.F1
ms.assetid: 8c9bb3b3-ea77-4a5b-ba35-7451ed11083d
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 4c8ff22e9edee8af2af4b948289b56c3078e4232
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089018"
---
# <a name="database-ssrs-native-mode"></a>데이터베이스(SSRS 기본 모드)
  데이터베이스 페이지에서는 하나 이상의 보고서 서버 인스턴스에 내부 저장소를 제공하는 보고서 서버 데이터베이스를 만들어 구성할 수 있습니다. 원격 보고서 서버 데이터베이스를 사용 하도록 보고서 서버를 구성 하는 경우 사용 해야는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager 데이터베이스를 만들 수 있습니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 보고서 서버 데이터베이스를 만들고 연결을 구성하려면 여러 단계를 수행해야 합니다. 이 페이지에서는 각 유형의 태스크에 대한 단계를 안내하는 마법사를 제공합니다. 사용 권한과 로그인은 자동으로 생성되거나 업데이트됩니다. 각 단계의 상태는 진행률 페이지에서 모니터링할 수 있습니다. 오류가 발생할 경우 오류를 클릭하면 해결 방법을 볼 수 있습니다.  
  
 보고서 서버 데이터베이스는 특정 서버 모드를 지원해야 합니다. 기본 모드는 기본 모드이지만 SharePoint 제품 또는 기술에 대한 대규모 배포에서 보고서 서버를 실행하는 경우에는 SharePoint 통합 모드용으로 보고서 서버 데이터베이스를 만들 수도 있습니다. 자세한 내용은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.  
  
 이 페이지를 열려면 시작는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager와 클릭 **데이터베이스** 탐색 창에서. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **SQL Server 이름**  
 현재 보고서 서버 데이터베이스에 **SQL Server 이름** 의 이름을 지정는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 하는 보고서 서버 데이터베이스를 실행 합니다. 로컬 컴퓨터나 원격 컴퓨터에서 기본 또는 명명된 인스턴스를 사용할 수 있습니다.  
  
 **Database Name**  
 서버 데이터를 저장하는 보고서 서버 데이터베이스의 이름을 지정합니다.  
  
 **보고서 서버 모드**  
 보고서 서버 데이터베이스가 기본 모드를 지원하는지, 아니면 SharePoint 통합 모드를 지원하는지를 나타냅니다. 자세한 내용은 참조 [Reporting Services 보고서 서버](../../../2014/reporting-services/reporting-services-report-server.md)합니다.  
  
 **데이터베이스 변경**  
 보고서 서버 데이터베이스를 만들거나 선택하는 데 필요한 모든 단계를 안내하는 마법사가 시작됩니다.  
  
 **자격 증명 유형**  
 보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 사용하는 자격 증명을 지정합니다. 서비스 계정, Windows 도메인 사용자, Windows 로컬 사용자 지정할 수 있는 자격 증명 유형은 포함 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인입니다. 자격 증명을 선택 하는 방법에 대 한 자세한 내용은 참조 [보고서 서버 데이터베이스 연결 구성 &#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)합니다.  
  
 **사용자 이름**  
 Windows 자격 증명을 사용 하는 경우 또는 도메인 사용자 계정을 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하는 경우 로그인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명입니다. Windows 자격 증명을 사용 하는 경우이 형식에 지정:  *\<도메인 >\\< 계정\>* 합니다.  
  
 **암호**  
 계정의 암호를 지정합니다.  
  
 **자격 증명 변경**  
 다른 계정을 선택하거나 보고서 서버 데이터베이스에 연결하는 데 사용되는 계정에 대한 암호를 업데이트하는 데 필요한 모든 단계를 안내하는 마법사가 시작됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [보고서 서버 데이터베이스&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [보고서 서버 데이터베이스 연결 구성 &#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  