---
title: 자격 증명 변경 마법사 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 632cfe6f1ea61612f59225f38a665ef73da0d898
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078500"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>자격 증명 변경 마법사(SSRS 기본 모드)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 보고서 서버 데이터베이스에 연결할 때 보고서 서버에서 사용하는 계정을 다시 구성하는 단계를 안내하는 자격 증명 변경 마법사를 제공합니다. 자격 증명을 변경할 때 구성 관리자는 보고서 서버에서 현재 사용 중인 보고서 서버 데이터베이스의 데이터베이스 서버에 대한 모든 사용 권한과 데이터베이스 로그인 정보를 업데이트합니다.  
  
 마법사를 시작 하려면 **자격 증명 변경** 의 데이터베이스 페이지에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager입니다. 시작 하는 방법에 대 한 지침은 합니다 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 참조 하세요 [Reporting Services 구성 관리자 &#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)합니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
## <a name="options"></a>변수  
 **데이터베이스 서버**  
 이름을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 보고서 서버 데이터베이스를 실행 하는 인스턴스.  
  
 에 연결 하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스, 데이터베이스 정보를 업데이트 하 고 서버에 로그온 할 권한이 있는 자격 증명을 사용 해야 합니다. 합니다 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager는 현재 Windows 자격 증명을 사용 하지만 로그인 또는 데이터베이스 권한이 없는 경우 지정할 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인입니다.  
  
 다른 Windows 자격 증명은 지정할 수 없습니다. 다른 Windows 사용자가 해당 사용자로 로그인으로 연결 하 고 시작 하려는 경우는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager입니다.  
  
 **자격 증명**  
 보고서 서버가 보고서 서버 데이터베이스에 연결할 때 사용하는 계정을 지정합니다. 유효한 값은 보고서 서버 웹 서비스의 서비스 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 정의 된 데이터베이스 로그인을 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스는 Windows 계정 또는 보고서 서버를 호스트 하는 데 사용할 합니다. Windows 계정을 사용 하는 경우 로컬 계정을 지정할 수 있습니다 (*\<컴퓨터 이름 >\\< 사용자 이름\>*) 동일한 컴퓨터 또는 도메인 사용자를 보고서 서버 및 데이터베이스에 있는 경우 계정 (*\<도메인 >\\< 사용자 이름\>*) 하는 경우 동일한 도메인의 다른 컴퓨터에 있습니다.  
  
 그러면 보고서 서버에서 지정한 계정에 대한 데이터베이스 로그인을 만들고 데이터베이스 권한을 할당합니다.  
  
 보고서 서버에서 계정 자체를 만들지는 않습니다. 지정한 계정은 이미 있어야 하며 현재 배포 구성에 대해 유효해야 합니다. 특히 데이터베이스가 원격 컴퓨터에 있는 경우 Windows 계정을 사용하려면 해당 컴퓨터에 대한 로그온 권한이 있는 계정을 지정해야 합니다.  
  
 컴퓨터를 다른 도메인 이나 트러스트 되지 않은 도메인에 있으면 사용해는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인입니다. 계정을 선택 하는 방법에 대 한 자세한 내용은 참조 하세요. [보고서 서버 데이터베이스 연결 구성 &#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)합니다.  
  
 **요약**  
 마법사가 실행되기 전에 설정을 확인합니다.  
  
 **진행 후 마침**  
 각 태스크의 진행률을 모니터링합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [데이터베이스 변경 마법사 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [보고서 서버 데이터베이스 연결 구성 &#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
