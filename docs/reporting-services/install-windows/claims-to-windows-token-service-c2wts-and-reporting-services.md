---
title: "Windows 토큰 서비스 (c2WTS) 및 Reporting Services에 대 한 클레임 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2ab5f4b5d2774d9dc944ad17bb55063388b70a6d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>c2WTS(Windows 토큰 서비스에 대한 클레임) 및 Reporting Services

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  SharePoint 팜 외부에 있는 데이터 원본에 대해 Windows 인증을 사용하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에서 SharePoint c2WTS(Windows 토큰 서비스에 대한 클레임)를 사용해야 합니다. 사용자가 Windows 인증을 사용하여 데이터 원본에 액세스하는 경우에도 WFE(웹 프런트 엔드)와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스 간의 통신은 항상 클레임 인증으로 수행되기 때문에 SharePoint c2WTS가 필요합니다.  
  
 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있더라도 c2WTS가 필요합니다. 하지만 이 경우에는 제한된 위임이 필요하지 않습니다.  
  
 c2WTS에서 만들어진 토큰은 제한된 위임(특정 서비스로 제한됨)과 "모든 인증 프로토콜 사용" 구성 옵션에서만 작동합니다. 앞에서 설명한 것처럼 데이터 원본이 공유 서비스와 동일한 컴퓨터에 있으면 제한된 위임이 필요하지 않습니다.  
  
 사용자 환경에서 Kerberos 제한된 위임을 사용하는 경우 SharePoint Server 서비스와 외부 데이터 원본이 동일한 Windows 도메인에 있어야 합니다. c2WTS(Windows 토큰 서비스에 대한 클레임)를 사용하는 서비스는 c2WTS에서 Kerberos 프로토콜 전환을 사용하여 클레임을 Windows 자격 증명으로 변환할 수 있도록 Kerberos **제한된** 위임을 사용해야 합니다. 이러한 요구 사항은 모든 SharePoint 공유 서비스에 적용됩니다. 자세한 내용은 [SharePoint 2013에서 Kerberos 인증 계획](http://technet.microsoft.com/library/ee806870.aspx)을 참조하세요.  
  
 이 항목에 절차가 요약되어 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

> [!NOTE]
>  참고: 일부 구성 단계는 특정 팜 토폴로지에 따라 변경될 수 있으며 작동하지 않을 수도 있습니다. 예를 들어 단일 서버 설치에는 Windows Identity Foundation c2WTS 서비스가 지원되지 않으므로 이 팜 구성에서는 Windows 토큰 위임에 대한 클레임 시나리오가 가능하지 않습니다.

> [!IMPORTANT]
> 파워 뷰를 사용하여 파워 피벗 통합 문서에 대해 작업하는 경우 [Office Online Server 개요](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx)에 대한 추가 구성을 수행해야 합니다. 자세한 내용은 다음 백서를 참조하세요. 
>
> - [SharePoint 2016에서 SQL Server 2016 PowerPivot 및 파워 뷰 배포](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
> 
> - [다층 계층 SharePoint 2016 팜에서 SQL Server 2016 PowerPivot 및 파워 뷰 배포](../../analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm.md)
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>c2WTS를 구성하기 위해 필요한 기본 단계  
  
1.  c2WTS 서비스 계정을 구성합니다. c2WTS를 실행하는 각 응용 프로그램 서버의 로컬 관리자 그룹에 서비스 계정을 추가합니다. 또한 계정에 다음과 같은 로컬 보안 정책 권한이 있는지 확인합니다.  
  
    -   운영 체제의 일부로 작동  
  
    -   인증 후 클라이언트 가장  
  
    -   서비스로 로그온  
  
2.  c2WTS 서비스 계정에 대한 위임을 구성합니다. 계정에 대해 프로토콜 전환을 포함하는 제한된 위임을 구성해야 합니다. 또한 이 계정에는 통신해야 하는 서비스(예: SQL Server Engine, SQL Server Analysis Services)에 대한 위임 권한이 있어야 합니다. 위임을 구성하려는 경우 Active Directory 사용자 및 컴퓨터 스냅인을 사용할 수 있습니다.  

    > [!IMPORTANT]
    > 위임 탭에서 C2WTS 서비스 계정에 대해 어떤 설정을 구성하든 간에 Reporting Services 서비스 계정과 일치해야 합니다. 예를 들어 C2WTS 서비스 계정이 SQL 서비스에 위임할 수 있게 하는 경우 Reporting Services 서비스 계정에 대해서도 동일한 작업을 수행해야 합니다.
  
    1.  각 서비스 계정을 마우스 오른쪽 단추로 클릭하고 속성 대화 상자를 엽니다. 대화 상자에서 **위임** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  참고: 개체에 SPN(서비스 사용자 이름)이 할당된 경우에만 위임 탭이 표시됩니다. c2WTS does not require an SPN on the c2WTS Account, however, without an SPN, the **위임** 탭이 표시되지 않습니다. 제한된 위임을 구성하는 다른 방법으로는 **ADSIEdit**와 같은 유틸리티를 사용할 수 있습니다.  
  
    2.  위임 탭에 대한 키 구성 옵션은 다음과 같습니다.  
  
        -   "지정한 서비스에 대한 위임용으로만 이 사용자 트러스트" 선택  
  
        -   "모든 인증 프로토콜 사용" 선택  

    3. **추가** 를 선택하여 위임할 서비스를 추가합니다.
    
    4. 선택 **사용자 또는 컴퓨터...** *는 서비스를 호스트 하는 계정을 입력 합니다. 예를 들어, SQL Server 명명 된 계정에서 실행 중인 경우 *sqlservice*, 입력 `sqlservice`합니다.
    
    5. 서비스 목록을 선택합니다. 해당 계정에서 사용할 수 있는 SPN이 표시됩니다. 해당 계정에 서비스가 표시되지 않는 경우 누락되었거나 다른 계정에 배치되었을 수 있습니다. SetSPN 유틸리티를 사용하여 SPN을 조정할 수 있습니다.
    
    6. 확인을 선택하여 대화 상자를 종료합니다.
  
3.  c2WTS 'AllowedCallers' 구성  
  
     c2WTS에는 구성 파일 **c2WTShost.exe.config**에 명시적으로 나열된 'callers' ID가 필요합니다. c2WTS는 특별히 구성되지 않은 한 시스템의 모든 인증된 사용자로부터의 요청을 허용하지 않습니다. 이 경우 'caller'는 WSS_WPG Windows 그룹입니다. c2WTShost.exe.config 파일은 다음 위치에 저장됩니다.  
     
     > [!NOTE]
     > SharePoint 중앙 관리 내에서 C2WTS 서비스에 대한 서비스 계정을 변경하면 WSS_WPG 그룹에 해당 계정이 추가됩니다.
  
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
4.  SharePoint 'Windows 토큰 서비스에 대한 클레임' 시작: **서버의 서비스 관리** 페이지에서 SharePoint 중앙 관리를 통해 Windows 토큰 서비스에 대한 클레임을 시작합니다. 서비스는 동작을 수행하는 서버에서 시작되어야 합니다. 예를 들어 WFE인 서버와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스가 실행되는 응용 프로그램 서버인 다른 서버가 있는 경우 응용 프로그램 서버에서만 c2WTS를 시작하면 됩니다. WFE에는 c2WTS가 필요하지 않습니다.

## <a name="next-steps"></a>다음 단계

[C2WTS(Windows 토큰 서비스에 대한 클레임) 개요](http://msdn.microsoft.com/library/ee517278.aspx)   
[SharePoint 2013에서 Kerberos 인증 계획](http://technet.microsoft.com/library/ee806870.aspx)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
