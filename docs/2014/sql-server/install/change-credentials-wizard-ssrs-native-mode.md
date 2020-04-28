---
title: 자격 증명 변경 마법사 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 07ca904ab8f98dd4dcbdba3f18f4a6fc6469f26a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952325"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>자격 증명 변경 마법사(SSRS 기본 모드)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 보고서 서버 데이터베이스에 연결할 때 보고서 서버에서 사용하는 계정을 다시 구성하는 단계를 안내하는 자격 증명 변경 마법사를 제공합니다. 자격 증명을 변경할 때 구성 관리자는 보고서 서버에서 현재 사용 중인 보고서 서버 데이터베이스의 데이터베이스 서버에 대한 모든 사용 권한과 데이터베이스 로그인 정보를 업데이트합니다.  
  
 마법사를 시작하려면 **구성 관리자의 데이터베이스 페이지에서** 자격 증명 변경 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 을 클릭합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager를 시작 하는 방법에 대 한 지침은 [Reporting Services 구성 관리자 &#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)를 참조 하세요.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
## <a name="options"></a>옵션  
 **데이터베이스 서버**  
 보고서 서버 데이터베이스를 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 하는 인스턴스의 이름을 지정 합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하려면 서버에 로그온하여 데이터베이스 정보를 업데이트할 권한이 있는 자격 증명을 사용해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 사용자의 현재 Windows 자격 증명을 사용하지만 사용자에게 로그인 또는 데이터베이스 권한이 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인을 지정할 수 있습니다.  
  
 다른 Windows 자격 증명은 지정할 수 없습니다. 다른 Windows 사용자로 연결하려면 해당 사용자로 로그인한 다음 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작합니다.  
  
 **자격 증명**  
 보고서 서버가 보고서 서버 데이터베이스에 연결할 때 사용하는 계정을 지정합니다. 유효한 값으로는 보고서 서버 웹 서비스의 서비스 계정, 보고서 서버를 호스팅하는 데 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 정의된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 데이터베이스 로그인 또는 Windows 계정이 있습니다. Windows 계정을 사용 하는 경우 보고서 서버와 데이터베이스가 같은 컴퓨터에 있으면 로컬 계정 (*\<computername \\>\><username*)을 지정 하거나, 동일한 도메인의 다른 컴퓨터에 있는 경우 도메인 사용자 계정 (*\<도메인>\\<사용자 이름\>*)을 지정할 수 있습니다.  
  
 그러면 보고서 서버에서 지정한 계정에 대한 데이터베이스 로그인을 만들고 데이터베이스 권한을 할당합니다.  
  
 보고서 서버에서 계정 자체를 만들지는 않습니다. 지정한 계정은 이미 있어야 하며 현재 배포 구성에 대해 유효해야 합니다. 특히 데이터베이스가 원격 컴퓨터에 있는 경우 Windows 계정을 사용하려면 해당 컴퓨터에 대한 로그온 권한이 있는 계정을 지정해야 합니다.  
  
 컴퓨터가 다른 도메인이나 트러스트되지 않은 도메인에 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인을 사용하는 것이 좋습니다. 계정을 선택 하는 방법에 대 한 자세한 내용은 [보고서 서버 데이터베이스 연결 구성 &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)를 참조 하세요.  
  
 **요약**  
 마법사가 실행되기 전에 설정을 확인합니다.  
  
 **진행 후 마침**  
 각 태스크의 진행률을 모니터링합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSRS 기본 모드&#41;데이터베이스 &#40;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [SSRS 기본 모드 &#40;데이터베이스 변경 마법사&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [SSRS Configuration Manager &#40;기본 모드 보고서 서버 데이터베이스를 만듭니다&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
