---
title: 보고서 서버 초기화(구성 관리자) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], initializing
- initialization process [Reporting Services]
- checking report server initializations
- scale-out deployments [Reporting Services]
- initializing report servers [Reporting Services]
- verifying report server initializations
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 264159f4c892cc688b15293c0e4283fc46520720
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080832"
---
# <a name="ssrs-encryption-keys---initialize-a-report-server"></a>SSRS 암호화 키 - 보고서 서버 시작
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 초기화된 서버는 보고서 서버 데이터베이스의 데이터를 암호화하고 해독할 수 있는 서버입니다. 보고서 서버 작업을 위해서는 초기화가 필요합니다. 초기화는 보고서 서버 서비스가 처음 시작될 때 발생합니다. 또한 보고서 서버를 기존 배포에 참여시키거나 복구 프로세스의 일환으로 키를 수동으로 다시 만들 때도 발생합니다. 암호화 키를 사용하는 방법과 이유에 대한 자세한 내용은 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md) 및 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)을 참조하세요.  
  
 암호화 키는 부분적으로 보고서 서버 서비스의 프로필 정보를 기반으로 합니다. 보고서 서버 서비스를 실행하는 데 사용되는 사용자 ID를 변경한 경우 그에 맞게 키도 업데이트해야 합니다. Reporting Services 구성 도구를 사용하여 ID를 변경한 경우에는 이 단계가 자동으로 수행됩니다.  
  
 여타의 이유로 초기화가 실패하면 보고서 서버는 사용자 및 서비스 요청에 대한 응답으로 **RSReportServerNotActivated** 오류를 반환합니다. 이 경우 시스템 또는 서버 구성과 관련된 문제를 해결해야 할 수 있습니다. 자세한 내용은 [Troubleshoot issues and errors with Reporting Services(Reporting Services 문제 및 오류 해결)](https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx)(TechNet Wiki의 https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) )을 참조하세요.  
  
## <a name="overview-of-the-initialization-process"></a>초기화 프로세스의 개요  
 초기화 프로세스가 진행되면 암호화에 사용되는 대칭 키가 생성 및 저장됩니다. 대칭 키는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 암호화 서비스에 의해 생성되며 그런 다음 데이터 암호화 및 암호 해독을 위해 보고서 서버 서비스에 사용됩니다. 대칭 키는 비대칭 키와 함께 암호화됩니다.  
  
 초기화 프로세스는 다음과 같은 단계로 진행됩니다.  
  
1.  보고서 서버 서비스는 처음 시작될 때 RSReportServer.config 파일을 읽어 설치 식별자 및 데이터베이스 연결 정보를 가져옵니다.  
  
2.  보고서 서버 서비스가 암호화 서비스에서 공개 키를 요청합니다. Windows에서는 프라이빗 및 퍼블릭 키를 만든 후 퍼블릭 키를 보고서 서버 서비스로 보냅니다.  
  
3.  보고서 서버 서비스가 보고서 서버 데이터베이스에 연결한 후 설치 식별자와 공개 키 값을 저장합니다.  
  
4.  보고서 서버 서비스가 암호화 서비스를 호출하여 대칭 키를 요청합니다. Windows는 대칭 키를 만듭니다.  
  
5.  보고서 서버 서비스는 보고서 서버 데이터베이스에 다시 연결한 후 3단계에서 저장한 공개 키 및 설치 식별자 값에 대칭 키를 추가합니다. 보고서 서버 서비스는 대칭 키를 저장하기 전에 해당 공개 키를 사용하여 대칭 키를 암호화합니다. 대칭 키가 저장되면 보고서 서버는 초기화되어 사용 가능한 상태가 된 것입니다.  
  
## <a name="initializing-a-report-server-for-scale-out-deployment"></a>확장 배포를 위해 보고서 서버 초기화  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 여러 보고서 서버 인스턴스 간에 단일 보고서 서버 데이터베이스를 공유하는 스케일 아웃 배포 모델을 지원합니다. 스케일 아웃 배포에 참여하기 위해 보고서 서버는 대칭 키 복사본을 만들어 공유 데이터베이스에 저장해야 합니다. 해당 데이터베이스를 사용하는 서버에서는 단일 대칭 키를 사용해도 각 보고서 서버는 키의 자체 복사본을 보유합니다. 각 복사본은 공개 키를 사용하여 해당 소유자로 고유하게 암호화되므로 서로 다릅니다.  
  
 스케일 아웃 배포를 위해 보고서 서버를 초기화하는 처음 몇 단계는 단일 서버 및 데이터베이스 조합에 대한 초기화를 설명하는 처음 3단계와 동일합니다.  
  
 확장 배포를 위한 초기화 프로세스는 보고서 서버가 대칭 키를 가져오는 방식에서 차이를 보입니다. 첫 번째 서버는 초기화될 때 Windows에서 대칭 키를 가져옵니다. 스케일 아웃 배포를 위한 구성 중에 초기화된 두 번째 서버는 이미 초기화된 보고서 서버 서비스에서 대칭 키를 가져옵니다. 첫 번째 보고서 서버 인스턴스는 두 번째 인스턴스의 공개 키를 사용하여 두 번째 보고서 서버 인스턴스에 대해 대칭 키의 암호화된 복사본을 만듭니다. 이 과정 중에 대칭 키는 일반 텍스트로 절대 노출되지 않습니다.  
  
## <a name="how-to-initialize-a-report-server"></a>보고서 서버를 초기화하는 방법  
  
-   보고서 서버를 초기화하려면 Reporting Services 구성 도구를 사용합니다. 보고서 서버 데이터베이스를 만들어 구성하면 초기화가 자동으로 수행됩니다. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)의 지원되는 버전을 검토합니다.  
  
-   스케일 아웃 배포를 위해 보고서 서버를 초기화하려는 경우 Reporting Services 구성 도구나 **RSKeymgmt** 유틸리티에서 초기화 페이지를 사용할 수 있습니다. 단계별 지침을 따르려면 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
> [!NOTE]  
>  **RSKeymgmt**는 이미 스케일 아웃 배포에 포함된 보고서 서버 인스턴스를 호스트하는 컴퓨터의 명령줄에서 실행하는 콘솔 애플리케이션입니다. 이 유틸리티를 실행할 때는 인수를 지정하여 초기화할 원격 보고서 서버 인스턴스를 선택해야 합니다.  
  
 보고서 서버는 설치 식별자와 공개 키가 일치할 경우에만 초기화됩니다. 일치가 성공하면 해독 가능한 암호화를 허용하는 대칭 키가 만들어집니다. 일치가 실패하면 보고서 서버는 비활성화됩니다. 이 경우 백업 키를 적용하도록 요청되며 백업 키가 사용 불가능하거나 유효하지 않으면 암호화된 데이터를 삭제하도록 요청될 수 있습니다. 보고서 서버에서 사용하는 암호화 키에 대한 자세한 내용은 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI(Windows Management Instrumentation) 공급자를 사용하여 보고서 서버를 프로그래밍 방식으로 초기화할 수도 있습니다. 자세한 내용은 [Reporting Services WMI 공급자 액세스](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)를 참조하세요.  
  
## <a name="how-to-confirm-a-report-server-initialization"></a>보고서 서버 초기화를 확인하는 방법  
 보고서 서버 초기화를 확인하려면 명령 창에서 **https://\<servername>/reportserver**를 입력하여 보고서 서버 웹 서비스를 ping합니다. **RSReportServerNotActivated** 오류가 발생하면 초기화가 실패한 것입니다.  
  
## <a name="see-also"></a>참고 항목
[암호화 키 구성 및 관리(SSRS 구성 관리자)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)
  
  
