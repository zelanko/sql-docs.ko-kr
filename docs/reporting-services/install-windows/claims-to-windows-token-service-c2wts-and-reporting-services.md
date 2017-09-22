---
title: "Windows 토큰 서비스 (c2WTS) 및 Reporting Services에 대 한 클레임 | Microsoft Docs"
ms.custom: The Claims to Windows Token Service (C2WTS) is used by SharePoint and needs to be configured for Kerberos constrained delegation to work with SQL Server Reporting Services properly.
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: 8a478bba3cde66967594d5ef02f867de5b33edd7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/15/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>C2WTS(Windows 토큰 서비스에 대한 클레임) 및 Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

SharePoint 클레임 (C2WTS) Windows 토큰 서비스에는 기본 모드에서 보고서를 보려는 경우에 필요는 [SQL Server Reporting Services 보고서 뷰어 웹 파트](../report-server-sharepoint/deploy-report-viewer-web-part.md)합니다.

C2WTS은 SharePoint 팜 외부에 있는 데이터 원본에 대 한 Windows 인증을 사용 하려는 경우에 SQL Server Reporting Services SharePoint 모드 필요 합니다. 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있더라도 C2WTS가 필요합니다. 하지만 이 경우에는 제한된 위임이 필요하지 않습니다.

> [!NOTE]
> SQL Server 2016 후 SharePoint와 reporting Services 통합을 사용할 수 없습니다.

## <a name="report-viewer-web-part-configuration"></a>보고서 뷰어 웹 파트 구성

보고서 뷰어 웹 파트를 사용 하 여 SharePoint 사이트 내에서 SQL Server Reporting Services 기본 모드 보고서를 포함할 수 있습니다. 이 웹 파트는 SharePoint 2013 및 SharePoint 2016에 사용할 수 있습니다. SharePoint 2013 및 SharePoint 2016을 모두 확인 클레임 인증을 사용 합니다. 기본적으로 Windows 인증을 사용 하는 SQL Server Reporting Services (기본 모드). 결과적으로, C2WTS 올바르게 렌더링 하는 보고서에 대해 적절히 구성 해야 합니다.

## <a name="sharepoint-mode-integaration"></a>SharePoint 모드 integaration

**이 섹션에 SQL Server 2016 Reporting Services 및 이전 버전에 적용 됩니다.**

SharePoint 팜 외부에 있는 데이터 원본에 대 한 Windows 인증을 사용 하려는 경우 SharePoint 클레임 (C2WTS) Windows 토큰 서비스에 SQL Server Reporting Services SharePoint 모드 입력 해야 합니다. Reporting Services 공유 서비스 및 웹 프런트 엔드 간의 통신 WFE ()은 항상 클레임 인증 때문에 사용자가 Windows 인증을 사용 하 여 데이터 원본에 액세스 하는 경우에 마찬가지입니다.

## <a name="steps-needed-to-configure-c2wts"></a>C2WTS를 구성 하는 데 필요한 단계

C2WTS에서 만들어진 토큰은 제한된 위임(특정 서비스로 제한됨)과 "모든 인증 프로토콜 사용" 구성 옵션에서만 작동합니다. 앞에서 설명한 것처럼 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있으면 제한된 위임이 필요하지 않습니다.

사용자 환경에서 Kerberos 제한된 위임을 사용하는 경우 SharePoint Server 서비스와 외부 데이터 원본이 동일한 Windows 도메인에 있어야 합니다. c2WTS(Windows 토큰 서비스에 대한 클레임)를 사용하는 서비스는 c2WTS에서 Kerberos 프로토콜 전환을 사용하여 클레임을 Windows 자격 증명으로 변환할 수 있도록 Kerberos **제한된** 위임을 사용해야 합니다. 이러한 요구 사항은 모든 SharePoint 공유 서비스에 적용됩니다. 자세한 내용은 [SharePoint 2013에서 Kerberos 인증 계획](http://technet.microsoft.com/library/ee806870.aspx)을 참조하세요.  

1. C2WTS 서비스 계정을 구성 합니다. C2WTS에 사용 됨을 각 서버에서 로컬 관리자 그룹에 서비스 계정을 추가 합니다.

    에 대 한는 **보고서 뷰어 웹 파트**, 웹 WFE (프런트 엔드) 서버 사용 됩니다. 에 대 한 **SharePoint 통합된 모드**, Reporting Services 서비스가 실행 되 고 있는 응용 프로그램 서버 사용 됩니다.

2. C2WTS 서비스 계정에 대 한 위임을 구성 합니다.

    이 계정에는 제한 위임 프로토콜 전환 및 (즉, SQL Server 데이터베이스 엔진, SQL Server Analysis Services)와 통신 하는 데 필요한 서비스에 위임할 수 있는 권한이 필요 합니다. 위임을 구성 하려면 Active Directory 사용자 및 컴퓨터 스냅인 사용할 수 있으며 도메인 관리자가 되려면 필요 합니다.

    > [!IMPORTANT]
    > 모든 설정을 구성한 C2WTS 서비스 계정에 대 한 위임 탭에서 사용 되는 기본 서비스 계정와 일치 해야 합니다. 에 대 한는 **보고서 뷰어 웹 파트**, SharePoint 웹 응용 프로그램에 대 한 서비스 계정을이 됩니다. 에 대 한 **SharePoint 통합된 모드**, Reporting Services 서비스 계정을이 됩니다.
    >
    > 예를 들어 C2WTS 서비스 계정 SQL 서비스에 위임할 수를 허용 하는 경우 SharePoint 통합된 모드의 Reporting Services 서비스 계정에서 동일한 작업을 수행 해야 합니다.

    * 각 서비스 계정을 마우스 오른쪽 단추로 클릭하고 속성 대화 상자를 엽니다. 대화 상자에서 **위임** 탭을 클릭합니다.

        위임 탭만 개체에 서비스 사용자 이름 (SPN)에 할당 된 경우 표시 됩니다. 하지만 C2WTS an SPN, 없이 C2WTS 계정에 SPN을 필요 하지는 않습니다는 **위임** 탭 표시 되지 것입니다. 제한된 위임을 구성하는 다른 방법으로는 **ADSIEdit**와 같은 유틸리티를 사용할 수 있습니다.

    * 위임 탭에 대한 키 구성 옵션은 다음과 같습니다.

        * 선택 **지정한 서비스에 위임에 대해이 사용자 트러스트**
        * 선택 **모든 인증 프로토콜 사용**

    * **추가** 를 선택하여 위임할 서비스를 추가합니다.

    * 선택 **사용자 또는 컴퓨터... ***는 서비스를 호스트 하는 계정을 입력 합니다. 예를 들어, SQL Server 명명 된 계정에서 실행 중인 경우 *sqlservice*, 입력 `sqlservice`합니다. 

    * 서비스 목록을 선택합니다. 해당 계정에서 사용할 수 있는 SPN이 표시됩니다. 해당 계정에 서비스가 표시되지 않는 경우 누락되었거나 다른 계정에 배치되었을 수 있습니다. SetSPN 유틸리티를 사용하여 SPN을 조정할 수 있습니다.

    * 확인을 선택하여 대화 상자를 종료합니다.

3. C2WTS를 구성 *AllowedCallers*합니다.

    C2WTS ' id가 '를 명시적으로 필요한 구성 파일에 나열 된 **C2WTShost.exe.config**합니다. C2WTS는 특별히 구성되지 않은 한 시스템의 모든 인증된 사용자로부터의 요청을 허용하지 않습니다. 이 경우 ' c'는 WSS_WPG Windows 그룹입니다. C2WTShost.exe.confi 파일은 다음 위치에 저장 됩니다.

    SharePoint 중앙 관리 내에서 C2WTS 서비스에 대한 서비스 계정을 변경하면 WSS_WPG 그룹에 해당 계정이 추가됩니다.

    **\Program Files\Windows Identity Foundation\v3.5\c2WTShost.exe.config**

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

4. SharePoint 중앙 관리를 통해 Windows 토큰 서비스에 대 한 클레임에서 시작 된 **서버의 서비스 관리** 페이지. 서비스는 동작을 수행하는 서버에서 시작되어야 합니다. 예를 들어 서버 응용 프로그램 서버에서 C2WTS를 시작 하는 WFE / 응용 프로그램 서버를 실행 하는 SQL Server Reporting Services 공유 서비스에만 상태가 다른 서버에 필요 합니다. 보고서 뷰어 웹 파트를 실행 하는 경우 WFE 서버에서 C2WTS 하기만 됩니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
