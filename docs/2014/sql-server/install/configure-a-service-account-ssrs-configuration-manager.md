---
title: 서비스 계정 (SSRS 구성 관리자) 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Server Web service, accounts
- service accounts [Reporting Services]
- Report Server Windows service, accounts
- Web service [Reporting Services], report server
ms.assetid: 25000ad5-3f80-4210-8331-d4754dc217e0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0ffc525e4d9ab516481eadf4cc303a704ce56da6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136383"
---
# <a name="configure-a-service-account-ssrs-configuration-manager"></a>서비스 계정 구성(SSRS 구성 관리자)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치에서 보고서 서버 웹 서비스, 보고서 관리자 및 백그라운드 처리 응용 프로그램은 하나의 서비스 내에서 실행됩니다. 서비스를 실행하는 계정은 설치 중 서비스 ID 페이지에 계정을 지정할 때 정의되지만 다른 계정을 사용하거나 암호를 업데이트하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용할 수 있습니다.  
  
 보고서 서버가 SharePoint 통합 모드를 사용 하도록 구성 된 및 사용 하 여 서비스 계정을 변경 하는 경우는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구, 있습니다 해야 SharePoint 중앙 관리를 열어 합니다 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  **데이터베이스 액세스 권한 부여** 페이지에서 보고서 서버 및 인스턴스 설정을 다시 적용 합니다. 이 단계 액세스 권한이 부여 됩니다 새 서비스 계정에 SharePoint 데이터베이스에 통합 하는 데 필요한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 사용 하 여 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]합니다.  
  
 서비스 계정을 업데이트할 때는 서비스 ID에 종속된 다른 설정도 함께 업데이트되도록 항상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하십시오.  
  
> [!NOTE]  
>  도메인 컨트롤러인 컴퓨터에서는 기본 제공 Windows 서비스 계정(로컬 서비스 또는 네트워크 서비스)이 보고서 서버 서비스 계정으로 지원되지 않습니다.  
  
 절차  
  
### <a name="to-configure-the-report-server-service-account"></a>보고서 서버 서비스 계정을 구성하려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작한 후 보고서 서버에 연결합니다.  
  
2.  서비스 계정 페이지에서 사용하려는 계정 유형에 해당하는 옵션을 선택합니다. 내용은 지정할 계정 유형에 대 한 권장 사항은 [보고서 서버 서비스 계정 구성 &#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)합니다.  
  
3.  Windows 사용자 계정을 선택한 경우 새 계정과 암호를 지정합니다. 계정은 20자를 초과할 수 없습니다.  
  
     보고서 서버가 Kerberos 인증을 지원하는 네트워크에 배포된 경우 방금 지정한 도메인 사용자 계정으로 보고서 서버 SPN(서비스 사용자 이름)을 등록해야 합니다. 자세한 내용은 [보고서 서버의 SPN&#40;서비스 사용자 이름&#41; 등록](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)을 참조하세요.  
  
4.  **적용**을 클릭합니다.  
  
5.  대칭 키를 백업하라는 메시지가 표시되면 대칭 키를 백업할 파일 이름과 위치를 입력하고 파일을 잠그거나 잠금 해제할 때 사용할 암호를 입력한 다음 **확인**을 클릭합니다.  
  
6.  보고서 서버에서 서비스 계정을 사용하여 보고서 서버 데이터베이스에 연결하는 경우 새 계정 또는 암호를 사용하도록 연결 정보가 업데이트됩니다. 연결 정보를 업데이트하려면 데이터베이스에 연결해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **데이터베이스 연결** 대화 상자가 나타나면 데이터베이스에 연결할 권한이 있는 자격 증명을 입력한 다음 **확인**을 클릭합니다.  
  
7.  대칭 키를 복원하라는 메시지가 표시되면 5단계에서 지정한 암호를 입력한 다음 **확인**을 클릭합니다.  
  
8.  결과 창에서 상태 메시지를 검토하여 모든 태스크가 성공적으로 완료되었는지 확인합니다.  
  
## <a name="troubleshooting-service-identity-update-errors"></a>서비스 ID 업데이트 오류 문제 해결  
 서비스 ID를 변경하면 서비스를 다시 시작하고 암호로 보호된 암호화 키, URL 예약 및 보고서 서버 데이터베이스 연결 정보(서비스 계정을 사용하여 보고서 서버 데이터베이스에 연결하는 경우)를 업데이트하는 일련의 이벤트가 시작됩니다. 이러한 이벤트의 상태는 페이지 아래쪽에 있는 결과 창의 알림을 통해 모니터링할 수 있습니다. 이 프로세스 도중 오류가 발생하면 다음 방법을 사용하여 오류를 해결할 수 있습니다.  
  
-   대칭 키를 복원할 수 없는 경우 암호화 키 페이지의 **복원** 을 사용하여 수동으로 복원할 수 있습니다. 이 방법으로 해결되지 않으면 암호화된 내용을 삭제합니다. 이 경우 데이터 원본 연결 정보와 구독은 다시 만들어야 하지만 나머지 내용은 그대로 사용할 수 있습니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.  
  
-   서비스가 시작되지 않는 경우 관리 도구의 서비스 콘솔 응용 프로그램을 사용하여 수동으로 서비스를 다시 시작합니다.  
  
-   서비스 계정을 업데이트할 때 URL 예약 오류가 발생할 수 있습니다. 각 URL 예약에는 서비스 계정에 URL 요청을 수락할 권한을 부여하는 DACL(임의 액세스 제어 목록)이 포함된 보안 설명자가 있습니다. 계정을 업데이트할 때 URL을 다시 만들어 새 계정 정보로 DACL을 업데이트해야 합니다. URL 예약을 다시 만들 수 없지만 올바른 계정임이 확실한 경우에는 컴퓨터를 다시 시작합니다. 그래도 오류가 계속되면 다른 계정을 사용해 보십시오.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자 &#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [보고서 서버 데이터베이스 연결 구성 &#40;SSRS 구성 관리자&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [서비스 계정 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/service-account-ssrs-native-mode.md)   
 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
