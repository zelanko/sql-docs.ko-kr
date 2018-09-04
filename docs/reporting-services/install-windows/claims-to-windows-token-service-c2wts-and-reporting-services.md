---
title: c2WTS(Windows 토큰 서비스에 대한 클레임) 및 Reporting Services | Microsoft Docs
ms.date: 09/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.suite: pro-bi
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a4092aa6f801d1f3f521cffc088e8b345495267b
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43275610"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>C2WTS(Windows 토큰 서비스에 대한 클레임) 및 Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

SharePoint C2WTS(Windows 토큰 서비스에 대한 클레임)는 [SQL Server Reporting Services 보고서 뷰어 웹 파트](../report-server-sharepoint/deploy-report-viewer-web-part.md) 내에서 기본 모드 보고서를 보려는 경우에 필요합니다.

SharePoint 팜 외부에 있는 데이터 원본에 대해 Windows 인증을 사용하려면 SQL Server Reporting Services SharePoint 모드에서 C2WTS를 사용해야 합니다. 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있더라도 C2WTS가 필요합니다. 하지만 이 경우에는 제한된 위임이 필요하지 않습니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

## <a name="report-viewer-web-part-configuration"></a>보고서 뷰어 웹 파트 구성

보고서 뷰어 웹 파트를 SharePoint 사이트 내에서 SQL Server Reporting Services 기본 모드 보고서를 포함하는 데 사용할 수 있습니다. 이 웹 파트는 SharePoint 2013 및 SharePoint 2016에서 사용할 수 있습니다. SharePoint 2013 및 SharePoint 2016은 모두 클레임 인증을 사용합니다. SQL Server Reporting Services(기본 모드)는 기본적으로 Windows 인증을 사용합니다. 결과적으로, C2WTS를 보고서에 대해 적절하게 구성해야 올바르게 렌더링할 수 있습니다.

## <a name="sharepoint-mode-integaration"></a>SharePoint 모드 통합

**이 섹션은 SQL Server 2016 Reporting Services 및 이전 버전에 적용됩니다.**

SharePoint 팜 외부에 있는 데이터 원본에 대해 Windows 인증을 사용하려면 SQL Server Reporting Services SharePoint 모드에서 SharePoint C2WTS(Windows 토큰 서비스에 대한 클레임)를 사용해야 합니다. 사용자가 Windows 인증을 사용하여 데이터 원본에 액세스하는 경우에도 WFE(웹 프런트 엔드)와 Reporting Services 공유 서비스 간의 통신은 항상 클레임 인증으로 수행되기 때문에 SharePoint c2WTS가 필요합니다.

## <a name="steps-needed-to-configure-c2wts"></a>c2WTS를 구성하기 위해 필요한 단계

C2WTS에서 만들어진 토큰은 제한된 위임(특정 서비스로 제한됨)과 "모든 인증 프로토콜 사용" 구성 옵션에서만 작동합니다. 앞에서 설명한 것처럼 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있으면 제한된 위임이 필요하지 않습니다.

사용자 환경에서 Kerberos 제한된 위임을 사용하는 경우 SharePoint Server 서비스와 외부 데이터 원본이 동일한 Windows 도메인에 있어야 합니다. c2WTS(Windows 토큰 서비스에 대한 클레임)를 사용하는 서비스는 c2WTS에서 Kerberos 프로토콜 전환을 사용하여 클레임을 Windows 자격 증명으로 변환할 수 있도록 Kerberos **제한된** 위임을 사용해야 합니다. 이러한 요구 사항은 모든 SharePoint 공유 서비스에 적용됩니다. 자세한 내용은 [SharePoint 2013에서 Kerberos 인증 계획](http://technet.microsoft.com/library/ee806870.aspx)을 참조하세요.  

1. C2WTS 서비스 계정을 구성합니다. C2WTS를 사용하는 각 서버의 로컬 관리자 그룹에 서비스 계정을 추가합니다.

    **보고서 뷰어 웹 파트**의 경우, WFE(웹 프런트 엔드) 서버가 사용됩니다. **SharePoint 통합 모드**의 경우, Reporting Services 서비스가 실행되고 있는 응용 프로그램 서버가 사용됩니다.

2. C2WTS 서비스 계정에 대한 위임을 구성합니다.

    계정에 대해 프로토콜 전환을 포함하는 제한된 위임을 구성해야 합니다. 또한 이 계정에는 통신해야 하는 서비스(예: SQL Server Database Engine, SQL Server Analysis Services)에 대한 위임 권한이 있어야 합니다. 위임을 구성하려는 경우 Active Directory 사용자 및 컴퓨터 스냅인을 사용할 수 있으며 도메인 관리자여야 합니다.

    > [!IMPORTANT]
    > 위임 탭에서 C2WTS 서비스 계정에 대해 어떤 설정을 구성하든 간에 사용 중인 주 서비스 계정과 일치해야 합니다. **보고서 뷰어 웹 파트**의 경우, SharePoint 웹 응용 프로그램에 대한 서비스 계정입니다. **SharePoint 통합 모드**의 경우, Reporting Services 서비스 계정입니다.
    >
    > 예를 들어 C2WTS 서비스 계정이 SQL 서비스에 위임할 수 있게 하는 경우 SharePoint 통합 모드에 대한 Reporting Services 서비스 계정에 대해서도 동일한 작업을 수행해야 합니다.

    * 각 서비스 계정을 마우스 오른쪽 단추로 클릭하고 속성 대화 상자를 엽니다. 대화 상자에서 **위임** 탭을 클릭합니다.

        개체에 SPN(서비스 사용자 이름)이 할당된 경우에만 위임 탭이 표시됩니다. C2WTS는 C2WTS 계정에서 SPN이 필수는 아니지만 SPN이 없을 경우 **위임** 탭이 표시되지 않습니다. 제한된 위임을 구성하는 다른 방법으로는 **ADSIEdit**와 같은 유틸리티를 사용할 수 있습니다.

    * 위임 탭에 대한 키 구성 옵션은 다음과 같습니다.

        * **지정한 서비스에 대한 위임용으로만 이 사용자 트러스트** 선택
        * **모든 인증 프로토콜 사용** 선택

    * **추가** 를 선택하여 위임할 서비스를 추가합니다.

    * **사용자 또는 컴퓨터...***를 선택하고 서비스를 호스트하는 계정을 입력합니다. 예를 들어 *sqlservice*라는 계정으로 SQL Server를 실행 중이면 `sqlservice`를 입력합니다. 

    * 서비스 목록을 선택합니다. 해당 계정에서 사용할 수 있는 SPN이 표시됩니다. 해당 계정에 서비스가 표시되지 않는 경우 누락되었거나 다른 계정에 배치되었을 수 있습니다. SetSPN 유틸리티를 사용하여 SPN을 조정할 수 있습니다.

    * 확인을 선택하여 대화 상자를 종료합니다.

3. C2WTS *AllowedCallers*를 구성합니다.

    C2WTS에는 구성 파일 **C2WTShost.exe.config**에 명시적으로 나열된 ‘callers’ ID가 필요합니다. C2WTS는 특별히 구성되지 않은 한 시스템의 모든 인증된 사용자로부터의 요청을 허용하지 않습니다. 이 경우 ‘caller’는 WSS_WPG Windows 그룹입니다. C2WTShost.exe.config 파일은 다음 위치에 저장됩니다.

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

4. **서버의 서비스 관리** 페이지에서 SharePoint 중앙 관리를 통해 Windows 토큰 서비스에 대한 클레임을 시작합니다. 서비스는 동작을 수행하는 서버에서 시작되어야 합니다. 예를 들어 WFE인 서버와 SQL Server Reporting Services 공유 서비스가 실행되는 응용 프로그램 서버인 다른 서버가 있는 경우 응용 프로그램 서버에서만 C2WTS를 시작하면 됩니다. 보고서 뷰어 웹 파트를 실행하는 경우 C2WTS는 WFE 서버에서만 필요합니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
