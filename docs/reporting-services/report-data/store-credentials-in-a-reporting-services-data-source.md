---
title: Reporting Services 데이터 원본에 자격 증명 저장 | Microsoft Docs
description: 기본 모드 및 SharePoint 모드 보고서 서버 모두에서 저장된 자격 증명을 구성하는 방법을 알아봅니다.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 05/24/2018
ms.openlocfilehash: 18d9a5ad8c4df17525bad04f0b056e7f9c4f05ae
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478854"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Reporting Services 데이터 원본에 자격 증명 저장

::: moniker range="=sql-server-2016"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

::: moniker-end

::: moniker range=">=sql-server-2017"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]

::: moniker-end

보고서에 대한 외부 데이터에 액세스하기 위해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에서 사용하는 저장된 자격 증명을 구성할 수 있습니다. 보고서가 무인 모드로 실행되는 경우 저장된 자격 증명이 사용됩니다(예: 보고서를 전자 메일로 게시하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독). 보고서 처리가 예약되거나 트리거되면 보고서 서버는 자격 증명을 검색하고 사용합니다. 이 항목에서는 기본 모드 및 SharePoint 모드 보고서 서버에 대해 저장된 자격 증명을 구성하는 방법에 대해 설명합니다.  
  
##  <a name="security-policy-requirements-for-stored-credentials"></a><a name="bkmk_top"></a> 저장된 자격 증명에 대한 보안 정책 요구 사항  
 ![as_powerpivot_refresh_sss_set_key](/analysis-services/analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") 보고서 서버의 다음 보안 정책 중 하나의 경우, 저장된 자격 증명에 대해 사용하는 계정을 구성해야 합니다. 환경에서 필요한 최저 수준의 권한을 지닌 정책을 선택하는 것이 좋습니다.  
  
1.  **로컬 로그온 허용**. 자세한 내용은 [로컬 로그온 허용](https://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx)(영문)을 참조하세요.  
  
2.  **일괄 작업으로 로그온**. 자세한 내용은 [일괄 작업으로 로그온](https://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx)(영문)을 참조하세요.  
  
3.  정책에 대한 일반적인 정보는 [그룹 정책 개체의 보안 설정 편집](https://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx)(영문)을 참조하세요.  
  
##  <a name="configure-stored-credentials-for-a-report-specific-data-source-native-mode"></a><a name="bkmk_stored_credentials_data_source_native"></a> 보고서별 데이터 원본에 대해 저장된 자격 증명 구성(기본 모드)  
  
1.  웹 포털에서 보고서가 포함된 폴더로 이동합니다. 보고서 타일의 오른쪽 위 모서리에서 줄임표(...)를 클릭합니다.  
  
2.  **관리** 를 클릭한 다음 **데이터 원본** 을 클릭합니다.  
  
3.  **사용자 지정 데이터 원본** 을 선택합니다.  
  
4.  **데이터 원본 유형** 목록에서 데이터 원본의 데이터를 처리하는 데 사용할 데이터 처리 확장 프로그램을 선택합니다.  
  
5.  **연결 문자열** 에는 보고서 서버가 데이터 원본에 연결하는 데 사용하는 연결 문자열을 지정합니다. 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 연결하는 데 사용되는 연결 문자열을 보여 줍니다.  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  **연결 방법** 으로 **보고서 서버에 안전하게 저장된 자격 증명** 을 선택합니다.  
  
7.  사용자 이름 및 암호를 입력합니다.  
  
    -   계정이 Windows 도메인 사용자 계정인 경우 \<domain>\\<계정\> 형식으로 지정한 다음 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용** 을 선택합니다.  
  
    -   사용자 이름과 암호가 데이터베이스 자격 증명인 경우 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용** 을 선택하지 않습니다. 데이터베이스 서버가 가장 또는 위임을 지원하는 경우에는 **데이터 원본에 연결한 후 인증된 사용자로 가장** 을 선택할 수 있습니다.  
  
8.  **적용** 을 클릭합니다.  
  
     ![맨 위 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [저장된 자격 증명에 대한 보안 정책 요구 사항](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-report-specific-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_data_source_sharepoint"></a> 보고서별 데이터 원본에 대해 저장된 자격 증명 구성(SharePoint 모드)  
  
1.  보고서가 들어 있는 문서 라이브러리로 이동한 다음, 열기 메뉴 ![SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목")을 클릭합니다.  
  
2.  두 번째 열기 메뉴 ![SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목") 및 **데이터 원본 관리** 를 클릭합니다.  
  
3.  저장된 자격 증명으로 구성할 **사용자 지정** 데이터 원본의 이름을 클릭합니다.  
  
4.  **데이터 원본 유형** 목록에서 데이터 원본의 데이터를 처리하는 데 사용할 데이터 처리 확장 프로그램을 선택합니다.  
  
5.  **연결 문자열** 에는 보고서 서버가 데이터 원본에 연결하는 데 사용하는 연결 문자열을 지정합니다. 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 연결하는 데 사용되는 연결 문자열을 보여 줍니다.  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  **자격 증명** 에 대해 **저장된 자격 증명** 을 선택합니다.  
  
7.  **사용자 이름** 및 **암호** 를 입력합니다.  
  
    -   계정이 Windows 도메인 사용자 계정인 경우 \<domain>\\<계정\> 형식으로 지정한 다음 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용** 을 선택합니다.  
  
    -   사용자 이름과 암호가 데이터베이스 자격 증명인 경우 **Windows 자격 증명으로 사용** 을 선택하지 않습니다. 데이터베이스 서버에서 가장 또는 위임이 지원되는 경우 **실행 컨텍스트를 이 계정으로 설정** 을 선택할 수 있습니다.  
  
8.  **OK**(확인)를 클릭합니다.  
  
     ![맨 위 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [저장된 자격 증명에 대한 보안 정책 요구 사항](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-shared-data-source-native-mode"></a><a name="bkmk_stored_credentials_shared_data_source_native"></a> 공유 데이터 원본에 대해 저장된 자격 증명 구성(기본 모드)  
  
1.  웹 포털에서 공유 데이터 원본 항목을 찾습니다. 
  
2.  보고서 타일의 오른쪽 위 모서리 > **관리** 에서 줄임표(...)를 클릭합니다. 
  
3.  **유형** 목록에서 데이터 원본의 데이터를 처리하는 데 사용할 데이터 처리 확장 프로그램을 지정합니다.  
  
4.  **연결 문자열** 에는 보고서 서버가 데이터 원본에 연결하는 데 사용하는 연결 문자열을 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 연결 문자열에서 자격 증명을 지정하지 않는 것을 권장합니다.  
  
     다음 예에서는 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 연결하는 데 사용되는 연결 문자열을 보여 줍니다.  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  사용자 이름 및 암호를 입력합니다.  
  
    -   계정이 Windows 도메인 사용자 계정인 경우 \<domain>\\<계정\> 형식으로 지정한 다음 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용** 을 선택합니다.  
  
    -   사용자 이름과 암호가 데이터베이스 자격 증명인 경우 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용** 을 선택하지 않습니다. 데이터베이스 서버가 가장 또는 위임을 지원하는 경우에는 **데이터 원본에 연결한 후 인증된 사용자로 가장** 을 선택할 수 있습니다.  
  
6.  **적용** 을 클릭합니다.  
  
     ![맨 위 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [저장된 자격 증명에 대한 보안 정책 요구 사항](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-shared-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> 공유 데이터 원본에 대해 저장된 자격 증명 구성(SharePoint 모드)  
  
1.  문서 라이브러리에서 공유 데이터 원본 항목을 찾습니다.![공유 데이터 원본 아이콘](../../reporting-services/report-data/media/hlp-16datasource.png "공유 데이터 원본 아이콘")  
  
2.  바로 가기 메뉴인 ![SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목")을 클릭한 다음, 두 번째 바로 가기 메뉴인 ![SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "SSRS의 문서 라이브러리 상황에 맞는 메뉴 항목")을 클릭합니다.  
  
3.  **데이터 원본 정의 편집** 을 클릭합니다.  
  
4.  **데이터 원본 유형** 목록에서 데이터 원본의 데이터를 처리하는 데 사용할 데이터 처리 확장 프로그램을 지정합니다.  
  
5.  **연결 문자열** 에는 보고서 서버가 데이터 원본에 연결하는 데 사용하는 연결 문자열을 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 연결 문자열에서 자격 증명을 지정하지 않는 것을 권장합니다.  
  
     다음 예에서는 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 연결하는 데 사용되는 연결 문자열을 보여 줍니다.  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  사용자 이름 및 암호를 입력합니다.  
  
    -   계정이 Windows 도메인 사용자 계정인 경우 \<domain>\\<계정\> 형식으로 지정한 다음 **Windows 자격 증명으로 사용** 을 선택합니다.  
  
    -   사용자 이름과 암호가 데이터베이스 자격 증명인 경우 **Windows 자격 증명으로 사용** 을 선택하지 않습니다. 데이터베이스 서버에서 가장 또는 위임이 지원되는 경우 **실행 컨텍스트를 이 계정으로 설정** 을 선택할 수 있습니다.  
  
7.  **Ok** 를 클릭합니다.  
  
     ![맨 위 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [저장된 자격 증명에 대한 보안 정책 요구 사항](#bkmk_top)  
  
## <a name="see-also"></a>참고 항목  
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
