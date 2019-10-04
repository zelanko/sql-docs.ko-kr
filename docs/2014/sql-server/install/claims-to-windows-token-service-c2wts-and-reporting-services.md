---
title: C2WTS (Windows 토큰 서비스에 대 한 클레임) 및 Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 81bc6c12720d4b841e21191db5811d583d4c5edc
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952268"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>C2WTS(Windows 토큰 서비스에 대한 클레임) 및 Reporting Services
  The SharePoint Claims to Windows Token Service (c2WTS) is required with [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에 SharePoint C2WTS(Windows 토큰 서비스에 대한 클레임)가 필요합니다. 특히 사용자가 Windows 인증을 사용하여 데이터 원본에 액세스할 경우라도 WFE(웹 프런트 엔드)와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스 간의 통신은 항상 클레임 인증으로 수행되기 때문에 SharePoint C2WTS가 필요합니다.  
  
 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있더라도 C2WTS가 필요합니다. 하지만 이 경우에는 제한된 위임이 필요하지 않습니다.  
  
 c2WTS에서 만들어진 토큰은 제한된 위임(특정 서비스로 제한됨)과 "모든 인증 프로토콜 사용" 구성 옵션에서만 작동합니다. 앞에서 설명한 것처럼 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있으면 제한된 위임이 필요하지 않습니다.  
  
 사용자 환경에서 Kerberos 제한된 위임을 사용하는 경우 SharePoint Server 서비스와 외부 데이터 원본이 동일한 Windows 도메인에 있어야 합니다. c2WTS(Windows 토큰 서비스에 대한 클레임)를 사용하는 서비스는 c2WTS에서 Kerberos 프로토콜 전환을 사용하여 클레임을 Windows 자격 증명으로 변환할 수 있도록 Kerberos **제한된** 위임을 사용해야 합니다. 이러한 요구 사항은 모든 SharePoint 공유 서비스에 적용됩니다. 자세한 내용은 [Microsoft SharePoint 2010 제품용 Kerberos 인증 개요 (https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)을 참조 하세요.  
  
 이 항목에 절차가 요약되어 있습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
> [!NOTE]  
>  참고: 일부 구성 단계가 변경 되거나 특정 팜 토폴로지에서 작동 하지 않을 수 있습니다. 예를 들어 단일 서버 설치에는 Windows Identity Foundation C2WTS 서비스가 지원되지 않으므로 이 팜 구성에서는 Windows 토큰 위임에 대한 클레임 시나리오가 가능하지 않습니다.  
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>c2WTS를 구성하기 위해 필요한 기본 단계  
  
1.  c2WTS 서비스 계정을 구성합니다. c2WTS를 실행하는 각 애플리케이션 서버의 로컬 관리자 그룹에 서비스 계정을 추가합니다. 또한 계정에 다음과 같은 로컬 보안 정책 권한이 있는지 확인합니다.  
  
    -   운영 체제의 일부로 작동  
  
    -   인증 후 클라이언트 가장  
  
    -   서비스로 로그온  
  
     C2WTS에서 사용되는 계정은 프로토콜 전환을 포함하는 제한된 위임에 맞게 구성되어야 하며 통신해야 하는 서비스(예:SQL Server 엔진, SQL Server Analysis Services)에 대한 위임 권한이 필요합니다. 위임을 구성할 때는 Active Directory 사용자 및 컴퓨터 스냅인을 사용할 수 있습니다.  
  
    1.  각 서비스 계정을 마우스 오른쪽 단추로 클릭하고 속성 대화 상자를 엽니다. 대화 상자에서 **위임** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  참고: 개체에 SPN이 할당된 경우에만 위임 탭이 표시됩니다. c2WTS does not require an SPN on the c2WTS Account, however, without an SPN, the **위임** 탭이 표시되지 않습니다. 제한된 위임을 구성하는 다른 방법으로는 **ADSIEdit**와 같은 유틸리티를 사용할 수 있습니다.  
  
    2.  위임 탭에 대한 키 구성 옵션은 다음과 같습니다.  
  
        -   "지정한 서비스에 대 한 위임용 으로만이 사용자 트러스트"를 선택 합니다.  
  
        -   "모든 인증 프로토콜 사용" 선택  
  
         자세한 내용은 [SharePoint 2010 및 SQL Server 2008 R2 제품에 대 한 kerberos 인증 구성](http://blogs.technet.com/b/tothesharepoint/archive/2010/07/22/whitepaper-configuring-kerberos-authentication-for-sharepoint-2010-and-sql-server-2008-r2-products.aspx) 백서에서 "컴퓨터 및 서비스 계정에 대 한 kerberos 제한 된 위임 구성" 섹션을 참조 하십시오.  
  
2.  C2WTS ' AllowedCallers ' 구성  
  
     c2WTS에는 구성 파일 **c2wtshost.exe.config**에 명시적으로 나열 된 ' 호출자 ' id가 필요 합니다. c2WTS는이 작업을 수행 하도록 구성 되지 않은 한 시스템의 모든 인증 된 사용자 로부터의 요청을 허용 하지 않습니다. 이 경우 ‘caller’는 WSS_WPG Windows 그룹입니다. c2wtshost.exe.confi 파일은 다음 위치에 저장됩니다.  
  
     **\Program Files\Windows Identity Foundation\v3.5\c2wtshost.exe.config**  
  
     다음은 구성 파일의 예입니다.  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```  
  
3.  운영 체제의 C2WTS 서비스를 시작합니다.  
  
    1.  이전 단계에서 구성한 서비스 계정을 사용하도록 서비스를 구성합니다.  
  
    2.  시작 유형을 "**자동**"으로 변경 하 고 서비스를 시작 합니다.  
  
4.  SharePoint ' Windows 토큰 서비스에 대 한 클레임 '을 시작 합니다. **서버의 서비스 관리** 페이지에서 SharePoint 중앙 관리를 통해 Windows 토큰 서비스에 대한 클레임을 시작합니다. 서비스는 동작을 수행하는 서버에서 시작되어야 합니다. 예를 들어 WFE인 서버와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스가 실행되는 애플리케이션 서버인 다른 서버가 있는 경우 애플리케이션 서버에서만 c2WTS를 시작하면 됩니다. WFE에는 c2WTS가 필요하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [C2WTS (Windows 토큰 서비스에 대 한 클레임) 개요 (https://msdn.microsoft.com/library/ee517278.aspx)](https://msdn.microsoft.com/library/ee517278.aspx)   
 [Microsoft SharePoint 2010 제품에 대 한 Kerberos 인증 개요 (https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)  
  
  
