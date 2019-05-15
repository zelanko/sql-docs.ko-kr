---
title: 무인 실행 계정 구성(SSRS 구성 관리자) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- security [Reporting Services], unattended report processing
- unattended report processing [Reporting Services]
- credentials [Reporting Services]
- external data sources [Reporting Services]
- accounts [Reporting Services]
- reports [Reporting Services], processing
ms.assetid: 4e50733e-bd8c-4bf6-8379-98b1531bb9ca
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cdaf6447080a82d5b58932e7e4987720a97963b6
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65502942"
---
# <a name="configure-the-unattended-execution-account-ssrs-configuration-manager"></a>무인 실행 계정 구성(SSRS 구성 관리자)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 무인 모드로 보고서를 처리하고 네트워크를 통해 연결 요청을 전송하는 데 사용되는 특수 계정을 제공합니다. 이 계정은 다음과 같은 방법으로 사용됩니다.  
  
-   데이터베이스 인증을 사용하는 보고서에 대해 네트워크로 연결 요청을 전송하거나 인증을 요구 또는 사용하지 않는 외부 보고서 데이터 원본에 연결합니다. 자세한 내용은 SQL Server 온라인 설명서에서 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) 을 참조하세요.  
  
-   보고서에 사용되는 외부 이미지 파일 검색. 이미지 파일을 사용하려는 경우 익명 액세스를 통해 해당 파일에 액세스할 수 없으면 무인 모드로 실행되는 보고서 처리 계정을 구성하고 이 계정에 해당 파일에 액세스할 수 있는 권한을 부여할 수 있습니다.  
  
 무인 모드로 실행되는 보고서 처리란 사용자 요청 대신 이벤트(일정 기반 이벤트 또는 데이터 새로 고침 이벤트)에 의해 트리거되는 모든 보고서 실행 프로세스를 말합니다. 보고서 서버는 무인 모드로 실행되는 보고서 처리 계정을 사용하여 외부 데이터 원본을 호스팅하는 컴퓨터에 로그온합니다. 보고서 서버 서비스 계정의 자격 증명은 다른 컴퓨터에 연결할 때 사용되지 않으므로 이 계정이 필요합니다.  
  
> [!IMPORTANT]  
>  이 계정 구성은 선택 사항입니다. 그러나 계정을 구성하지 않는 경우 일부 데이터 원본에 연결하는 옵션이 제한되며 원격 컴퓨터에서 이미지 파일을 검색하지 못할 수 있습니다. 계정을 구성하는 경우 최신 상태로 유지해야 합니다. 특히 암호가 만료되도록 하거나 Active Directory에서 계정 정보를 변경하는 경우 다음에 보고서를 처리하면 "로그온하지 못했습니다(rsLogonFailed). 로그온 실패: 알 수 없는 사용자 이름이거나 암호가 틀립니다."와 같은 오류가 발생할 수 있습니다. 외부 이미지를 검색하거나 연결 요청을 외부 컴퓨터로 보내지 않는 경우에도 무인 모드로 실행되는 보고서 처리 계정을 적절하게 유지 관리해야 합니다. 계정을 구성한 다음 사용할 필요가 없게 되면 삭제하여 일상적인 계정 유지 관리 태스크를 수행하지 않을 수 있습니다.  
  
## <a name="how-to-configure-the-account"></a>계정 구성 방법  
 도메인 사용자 계정을 사용해야 합니다. 원래 용도대로 사용하려면 이 계정은 보고서 서버 서비스를 실행하는 데 사용되는 계정과 달라야 합니다. 보고서 서버에 데이터 원본 및 리소스를 제공하는 컴퓨터에 대해서만 최소 사용 권한(네트워크 연결 권한이 포함된 읽기 전용 액세스 권한이면 충분함)과 제한된 액세스 권한이 있는 계정을 사용해야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구 또는 **rsconfig** 유틸리티를 사용하여 계정을 지정할 수 있습니다. 무인 실행 계정을 구성하는 가장 쉬운 방법은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 실행하여 실행 계정 페이지에서 자격 증명을 지정하는 것입니다.  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 후 구성하려는 보고서 서버 인스턴스에 연결합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)를 참조하세요.  
  
2.  실행 계정 페이지에서 **실행 계정 지정**을 선택합니다.  
  
3.  계정 및 암호를 입력하고 암호를 다시 입력한 다음 **적용**을 클릭합니다.  
  
### <a name="using-rsconfig-utility"></a>RSCONFIG 유틸리티 사용  
 계정을 설정하는 다른 방법은 **rsconfig** 유틸리티를 사용하는 것입니다. 계정을 지정하려면 **rsconfig** 의 **-e**인수를 사용합니다. **rsconfig** 에 **-e** 인수를 지정하면 유틸리티가 계정 정보를 구성 파일에 기록합니다. RSreportserver.config에 대한 경로는 지정하지 않아도 됩니다. 다음 단계에 따라 계정을 구성합니다.  
  
1.  보고서 서버에 데이터 또는 서비스를 제공하는 컴퓨터와 서버에 액세스할 수 있는 도메인 계정을 만들거나 선택합니다. 축소된 권한(예: 읽기 전용 권한)을 가진 계정을 사용해야 합니다.  
  
2.  명령 프롬프트 열기: **시작** 메뉴에서 **실행**을 클릭한 다음 **cmd**를 입력하고 **확인**을 클릭합니다.  
  
3.  다음 명령을 입력하여 로컬 보고서 서버 인스턴스에서 계정을 구성합니다.  
  
     **rsconfig -e -u\<도메인/사용자 이름> -p\<암호>**  
  
 **rsconfig -e** 는 추가 인수를 지원합니다. 구문에 대한 자세한 내용 및 명령 예제를 보려면 SQL Server 온라인 설명서에서 [rsconfig 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)를 참조하세요.  
  
### <a name="how-account-information-is-stored"></a>계정 정보를 저장하는 방법  
 계정을 설정하면 로컬 또는 원격 보고서 서버 인스턴스의 RSreportserver.config 파일에 다음 설정이 암호화된 값으로 지정됩니다.  
  
```  
<UnattendedExecutionAccount>  
     <UserName></UserName>  
     <Password></Password>  
     <Domain></Domain>  
</UnattendedExecutionAccount>  
```  
  
 값을 설정한 후에는 암호를 해독하여 값을 일반 텍스트로 볼 수 없습니다. 값을 잘못 입력했거나 지정한 값이 기억나지 않는 경우 Reporting Services 구성 도구를 사용하거나 **rsconfig -e** 를 실행하여 처음부터 다시 시작해야 합니다.  
  
## <a name="how-to-use-the-unattended-report-processing-account"></a>무인 보고서 처리 계정을 사용하는 방법  
 보고서 서버는 자동으로 계정을 사용하여 이미지 파일을 검색하므로 사용자가 별도의 동작을 수행하지 않아도 됩니다. 보고서에 데이터를 제공하는 외부 데이터 원본에 연결하는 데 계정을 사용하려면 보고서 데이터 원본 또는 공유 데이터 원본의 데이터 원본 속성 페이지에서 **자격 증명 유형** 옵션을 지정해야 합니다.  
  
-   [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 또는 SharePoint 사이트에서 **자격 증명 필요 없음** 옵션을 선택합니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.
  
 무인 보고서 처리 계정은 기본적으로 데이터베이스 서버에 로그인할 때가 아닌 외부 서버에 연결할 때 사용됩니다. 이 계정 자격 증명을 사용하여 데이터베이스에 로그인하려면 연결 문자열에 자격 증명을 지정해야 합니다. 데이터베이스 서버가 Windows 통합 보안을 지원하고 무인 보고서 처리에 사용된 계정에 데이터베이스 읽기 권한이 있는 경우 **Integrated Security=SSPI** 를 지정할 수 있습니다. 그렇지 않은 경우, 연결 문자열에 사용자 이름 및 암호를 입력해야 하며 이것은 데이터 원본 연결 속성에 대한 편집 권한이 있는 모든 사용자에게 일반 텍스트로 표시됩니다.  
  
 연결을 설정한 후에 무인 보고서 처리 계정을 사용하여 데이터를 검색할 수 있지만 이 방법은 사용하지 않는 것이 좋습니다. 이 계정은 아주 특별한 기능을 위해 사용합니다. 데이터 검색에 이 계정을 사용하면 본래의 용도가 훼손될 수 있습니다.  
  
## <a name="how-to-maintain-the-unattended-report-processing-account"></a>무인 보고서 처리 계정을 유지 관리하는 방법  
 계정을 정의한 다음에는 계정과 암호를 최신 상태로 유지해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 이 계정에 대한 정보가 저장된 구성 설정을 업데이트할 수 있습니다.  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 후 구성하려는 보고서 서버 인스턴스에 연결합니다.  
  
2.  실행 계정 페이지에서 **실행 계정 지정** 이 선택되어 있는지 확인합니다.  
  
3.  새 계정 및 암호를 입력하고 암호를 다시 입력한 다음 **적용**을 클릭합니다.  
  
## <a name="how-to-delete-the-unattended-report-processing-account"></a>무인 보고서 처리 계정을 삭제하는 방법  
 계정을 사용할 필요가 없게 되면 삭제하여 일상적인 계정 유지 관리 태스크를 수행하지 않을 수 있습니다.  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 시작한 후 구성하려는 보고서 서버 인스턴스에 연결합니다.  
  
2.  실행 계정 페이지에서 **실행 계정 지정**의 선택을 취소합니다.  
  
3.  **적용**을 클릭합니다.  
  
 계정 정보가 RSReportServer.config 파일에서 제거됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 관리자(SSRS 기본 모드)](https://msdn.microsoft.com/379eab68-7f13-4997-8d64-38810240756e)  
  
  
