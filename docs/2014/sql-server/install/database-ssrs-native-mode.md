---
title: 데이터베이스 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.databasesetup.F1
ms.assetid: 8c9bb3b3-ea77-4a5b-ba35-7451ed11083d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4fc3fdb873a567bef9326232e5435cea5649b041
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054881"
---
# <a name="database-ssrs-native-mode"></a>데이터베이스(SSRS 기본 모드)
  데이터베이스 페이지에서는 하나 이상의 보고서 서버 인스턴스에 내부 스토리지를 제공하는 보고서 서버 데이터베이스를 만들어 구성할 수 있습니다. 원격 보고서 서버 데이터베이스를 사용하도록 보고서 서버를 구성하는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 데이터베이스를 만들어야 합니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]기본 모드입니다.  
  
 보고서 서버 데이터베이스를 만들고 연결을 구성하려면 여러 단계를 수행해야 합니다. 이 페이지에서는 각 유형의 태스크에 대한 단계를 안내하는 마법사를 제공합니다. 사용 권한과 로그인은 자동으로 생성되거나 업데이트됩니다. 각 단계의 상태는 진행률 페이지에서 모니터링할 수 있습니다. 오류가 발생할 경우 오류를 클릭하면 해결 방법을 볼 수 있습니다.  
  
 보고서 서버 데이터베이스는 특정 서버 모드를 지원해야 합니다. 기본 모드는 기본 모드이지만 SharePoint 제품 또는 기술에 대한 대규모 배포에서 보고서 서버를 실행하는 경우에는 SharePoint 통합 모드용으로 보고서 서버 데이터베이스를 만들 수도 있습니다. 자세한 내용은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.  
  
 이 페이지를 열려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작하고 탐색 창에서 **데이터베이스** 를 클릭합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **SQL Server 이름**  
 현재 보고서 서버 데이터베이스에서 **SQL Server 이름** 은 보고서 서버 데이터베이스를 실행하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 이름을 지정합니다. 로컬 컴퓨터나 원격 컴퓨터에서 기본 또는 명명된 인스턴스를 사용할 수 있습니다.  
  
 **데이터베이스 이름**  
 서버 데이터를 저장하는 보고서 서버 데이터베이스의 이름을 지정합니다.  
  
 **보고서 서버 모드**  
 보고서 서버 데이터베이스가 기본 모드를 지원하는지, 아니면 SharePoint 통합 모드를 지원하는지를 나타냅니다. 자세한 내용은 [Reporting Services Report Server](../../../2014/reporting-services/reporting-services-report-server.md)를 참조 하세요.  
  
 **데이터베이스 변경**  
 보고서 서버 데이터베이스를 만들거나 선택하는 데 필요한 모든 단계를 안내하는 마법사가 시작됩니다.  
  
 **자격 증명 유형**  
 보고서 서버에서 보고서 서버 데이터베이스에 연결할 때 사용하는 자격 증명을 지정합니다. 지정할 수 있는 자격 증명 유형은 서비스 계정, Windows 도메인 사용자, Windows 로컬 사용자 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인입니다. 자격 증명을 선택 하는 방법에 대 한 자세한 내용은 [보고서 서버 데이터베이스 연결 구성 &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)를 참조 하세요.  
  
 **사용자 이름**  
 Windows 자격 증명을 사용하는 경우 도메인 사용자 계정을 지정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다. Windows 자격 증명을 사용 하는 경우 * \<domain> \\<계정 \> *형식으로 지정 합니다.  
  
 **암호**  
 계정의 암호를 지정합니다.  
  
 **자격 증명 변경**  
 다른 계정을 선택하거나 보고서 서버 데이터베이스에 연결하는 데 사용되는 계정에 대한 암호를 업데이트하는 데 필요한 모든 단계를 안내하는 마법사가 시작됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSRS Configuration Manager &#40;기본 모드 보고서 서버 데이터베이스를 만듭니다&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [SSRS 기본 모드의 보고서 서버 데이터베이스 &#40;&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
