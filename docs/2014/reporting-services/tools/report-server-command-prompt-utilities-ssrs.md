---
title: 보고서 서버 명령 프롬프트 유틸리티(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fb8216c75ac29b01e527f5e0449330e51529b69e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191863"
---
# <a name="report-server-command-prompt-utilities-ssrs"></a>보고서 서버 명령 프롬프트 유틸리티(SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 보고서 서버를 관리하는 데 사용할 수 있는 몇 가지 명령줄 유틸리티가 포함되어 있습니다. 이러한 유틸리티는 보고서 서버를 설치할 때 자동으로 설치됩니다.  
  
|이름|명령 파일|지원되는 배포 모드|Description|  
|----------|------------------|-------------------------------|-----------------|  
|RSS 유틸리티|rs.exe|기본 모드 및 SharePoint 모드. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 릴리스에는 SharePoint 모드에 대한 지원이 도입되었습니다.|[rs 유틸리티](rs-exe-utility-ssrs.md) 는 스크립팅된 작업을 수행하는 데 사용할 수 있는 스크립트 호스트입니다. 이 도구를 사용하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 스크립트를 실행하여 보고서 서버 데이터베이스 간의 데이터 복사, 보고서 게시, 보고서 서버 데이터베이스에 항목 만들기 등을 수행할 수 있습니다. 스크립트를 사용하여 서버를 관리하는 방법에 대한 자세한 내용은 [배포 및 관리 태스크 스크립팅](script-deployment-and-administrative-tasks.md)을 참조하세요.|  
|Powershell cmdlet||SharePoint만|목록은 powershell cmdlet 참조 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md)합니다.|  
|rsconfig 유틸리티|rsconfig.exe|기본만|합니다 [rsconfig 유틸리티](rsconfig-utility-ssrs.md) 구성 및 보고서 서버 데이터베이스에 보고서 서버 연결을 관리 하는 데 사용 됩니다. 또한 무인 보고서 처리에 사용할 사용자 계정을 지정할 때도 이 유틸리티를 사용할 수 있습니다. 자세한 내용은 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../report-server/reporting-services-report-server-native-mode.md)를 참조하세요. 연결 구성에 대한 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)을 참조하세요.|  
|Rskeymgmt 유틸리티|rskeymgmt.exe|기본만|합니다 [rskeymgmt 유틸리티](rskeymgmt-utility-ssrs.md) 는 암호화 키 관리 도구입니다. 이 유틸리티를 사용하여 대칭 키를 백업하고, 적용하고, 다시 만들고, 삭제할 수 있습니다. 또한 공유 보고서 서버 데이터베이스에 보고서 서버 인스턴스를 연결할 때도 이 도구를 사용할 수 있습니다. 뿐만 아니라 데이터베이스 복구 작업에 사용할 수 있습니다. 대칭 키의 백업 복사본을 적용하여 새 설치에서 기존 데이터베이스를 다시 사용할 수 있습니다. 키를 복구할 수 없을 경우 이 도구는 더 이상 사용되지 않는 암호화된 내용을 삭제하는 방법을 제공합니다. 키 관리 및 중요한 데이터 저장에 대한 자세한 내용은 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md) 및 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)를 참조하세요.|  
  
> [!NOTE]  
>  그래픽 사용자 인터페이스가 있는 도구를 사용 하려는 경우 대신 Reporting Services 구성 관리자를 사용할 수 있습니다 `rsconfig` 고 `rskeymgmt`입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자 &#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 도구](reporting-services-tools.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../report-server/reporting-services-report-server-native-mode.md)  
  
  
