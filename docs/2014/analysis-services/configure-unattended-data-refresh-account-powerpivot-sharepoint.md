---
title: PowerPivot 무인 데이터 새로 고침 계정 구성 (SharePoint용 PowerPivot) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 81401eac-c619-4fad-ad3e-599e7a6f8493
author: minewiskan
ms.author: owend
ms.openlocfilehash: a7f373dfa85e80de6bfd3a0bb33e9b28ab33a697
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527249"
---
# <a name="configure-the-powerpivot-unattended-data-refresh-account-powerpivot-for-sharepoint"></a>PowerPivot 무인 데이터 새로 고침 계정 구성(SharePoint용 PowerPivot)
  PowerPivot 무인 데이터 새로 고침 계정은 SharePoint 팜에서 PowerPivot 데이터 새로 고침 작업을 실행할 용도로 지정된 계정입니다. 구성 하 여 데이터 새로 고침 일정 페이지에서 **관리자가 구성한 데이터 새로 고침 계정 사용** 옵션을 사용 하도록 설정 합니다 (아래 참조). 데이터 새로 고침을 예약한 통합 문서 만든 이가 PowerPivot 무인 데이터 새로 고침 계정을 사용하여 데이터 새로 고침 작업을 실행하려는 경우 이 옵션을 선택할 수 있습니다. 데이터 새로 고침 일정에서 자격 증명 옵션을 확인 하는 방법에 대 한 자세한 내용은 [데이터 새로 고침 예약 &#40;SharePoint용 PowerPivot&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)를 참조 하세요.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 서버를 구성할 때 선택한 옵션에 따라 무인 데이터 새로 고침 계정이 이미 만들어졌을 수도 있습니다. 기본 구성에서 무인 데이터 새로 고침 계정의 ID는 처음에 팜 계정으로 설정됩니다. 다른 사용자 권한으로 실행하도록 계정을 변경하여 배포 보안을 강화할 수 있습니다. 다음 지침에 따라 계정을 변경 합니다. [기존 PowerPivot 무인 데이터 새로 고침 계정에서 사용 하는 자격 증명을 업데이트](#bkmk_editUA)합니다.  
  
 모든 다른 설치 시나리오의 경우 아래 지침에 따라 중앙 관리에서 이 계정을 수동으로 구성해야 합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [필수 구성 요소](#bkmk_prereq)  
  
 [1 단계: 대상 응용 프로그램 만들기 및 자격 증명 설정](#bkmk_create)  
  
 [2 단계: PowerPivot 서버 구성 페이지에서 무인 계정 지정](#bkmk_specifyUA)  
  
 [3 단계: 계정에 참가 권한 부여](#bkmk_grant)  
  
 [4 단계: 데이터 새로 고침에 사용 되는 외부 데이터 원본에 액세스할 수 있는 읽기 권한 부여](#bkmk_dbread)  
  
 [5 단계: 데이터 새로 고침 구성 페이지에서 계정 가용성 확인](#bkmk_verify)  
  
 [PowerPivot 무인 데이터 새로 고침 계정 사용](#bkmk_use)  
  
 [기존의 PowerPivot 무인 데이터 새로 고침 계정에 사용되는 자격 증명 업데이트](#bkmk_editUA)  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> 전제 조건  
 보안 저장소 서비스를 사용하도록 설정하고 구성해야 하며 마스터 키를 생성해야 합니다. 이 작업을 수행 하는 방법에 대 한 지침은 [SharePoint 2010에서 PowerPivot 데이터 새로 고침](powerpivot-data-refresh-with-sharepoint-2010.md) 을 참조 하세요.  
  
 PowerPivot 무인 데이터 새로 고침 계정으로 사용할 Windows 도메인 사용자 계정을 미리 결정해야 합니다. 무인 데이터 새로 고침 용도로 만들어진 계정이어야 합니다. 그래야 계정이 사용되는 방식을 모니터링할 수 있습니다.  
  
 PowerPivot 시스템 서비스의 애플리케이션 ID를 알고 있어야 합니다. 이 서비스 계정에는 1 단계에서 대상 응용 프로그램을 만들 때 무인 데이터 새로 고침 계정에 대 한 **모든** 권한을 부여 합니다. 이러한 사용 권한이 있으면 PowerPivot 시스템 서비스에서는 데이터를 새로 고치는 동안 무인 데이터 새로 고침 계정의 자격 증명을 검색할 수 있습니다. 필요한 서비스 계정 정보를 얻으려면 중앙 관리에서 **서비스 계정 구성** 페이지를 열고 PowerPivot 서비스 응용 프로그램에서 사용 하는 서비스 응용 프로그램 풀을 선택 합니다. 기본적으로 **서비스 응용 프로그램 풀-SharePoint 웹 서비스 시스템**입니다.  
  
## <a name="configure-the-unattended-powerpivot-data-refresh-account"></a>무인 PowerPivot 데이터 새로 고침 계정 구성  
 PowerPivot 무인 데이터 새로 고침 계정은 PowerPivot 서비스 애플리케이션당 하나씩만 구성할 수 있습니다. 계정 정보는 보안 스토리지 서비스에서 미리 정의된 Windows 도메인 사용자 계정으로 설정된 대상 애플리케이션에 저장됩니다. 대상 애플리케이션이 만들어지면 PowerPivot 서비스 애플리케이션 구성 페이지에서 이를 PowerPivot 데이터 새로 고침 계정으로 지정할 수 있습니다.  
  
> [!NOTE]  
>  무인 데이터 새로 고침 계정에서 데이터 새로 고침이 수행될 때 무인 데이터 새로 고침에 사용된 Windows 사용자 계정에 대해 사용량 보고 및 데이터 새로 고침 기록이 기록됩니다. 데이터 새로 고침을 요청하거나 일정을 소유하는 각 개인에 대한 보다 정확한 기록이 필요할 경우 데이터 새로 고침을 실행하는 다른 옵션을 고려해 보십시오. 즉, 사용자에게 고유의 자격 증명을 지정하도록 하거나(기본값) 데이터 새로 고침용으로 사용할 Windows 자격 증명을 저장할 추가 대상 애플리케이션을 만들어 볼 수 있습니다. 자세한 내용은 [PowerPivot 데이터 새로 고침을 위한 저장 된 자격 증명 구성 &#40;SharePoint용 PowerPivot&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)을 참조 하십시오.  
  
 무인 데이터 새로 고침 계정 만들기 작업은 다섯 단계로 구성됩니다.  
  
-   Secure Store Service에서 계정에 대한 대상 애플리케이션을 만들고 자격 증명을 지정합니다.  
  
-   PowerPivot 서버 구성 페이지에서 무인 데이터 새로 고침 계정에 대한 대상 애플리케이션 ID를 지정합니다.  
  
-   계정에 참가 권한을 부여합니다.  
  
-   데이터를 새로 고치는 동안 외부 데이터 원본에 액세스할 수 있는 읽기 권한을 이 계정에 부여합니다.  
  
-   게시된 PowerPivot 통합 문서에 대한 데이터 새로 고침 관리 일정 페이지에서 계정이 사용 가능한지 확인합니다.  
  
###  <a name="step-1-create-a-target-application-and-set-the-credentials"></a><a name="bkmk_create"></a>1 단계: 대상 응용 프로그램 만들기 및 자격 증명 설정  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  **보안 저장소 서비스**를 클릭 합니다.  
  
3.  대상 응용 프로그램 관리에서 **새로 만들기**를 클릭 합니다.  
  
4.  대상 응용 프로그램 ID에 **PowerPivotDataRefresh**를 입력 합니다.  
  
5.  표시 이름에 **PowerPivot 데이터 새로 고침**을 입력 합니다.  
  
6.  담당자 전자 메일에 사용자의 전자 메일 주소를 입력합니다.  
  
7.  대상 응용 프로그램 형식에서 **개별**을 선택 합니다.  
  
    > [!NOTE]  
    >  PowerPivot 서비스 애플리케이션만 PowerPivot 무인 데이터 새로 고침 계정의 자격 증명을 요청하므로 이 시나리오에서는 개별 계정 유형을 지정하는 것이 맞습니다. 실무에서는 서비스 애플리케이션만 무인 데이터 새로 고침 계정을 사용하므로 이 대상 애플리케이션에서는 개별 계정 유형이 가장 적합합니다.  
  
8.  대상 애플리케이션 페이지 URL을 건너뜁니다. PowerPivot 데이터 새로 고침에서 이 URL을 사용하지 않습니다.  
  
9. **다음**을 클릭합니다.  
  
10. **보안 저장소 대상 응용 프로그램의 자격 증명 필드를 지정** 하십시오. 페이지에서 기본값을 적용 합니다. 필드 이름 및 유형은 Windows 사용자 이름 및 Windows 암호여야 합니다.  
  
11. **다음**을 클릭합니다.  
  
12. 대상 애플리케이션 관리자에서 PowerPivot 서비스 애플리케이션의 애플리케이션 풀 ID를 지정합니다. 런타임에 무인 데이터 새로 고침 계정 정보를 검색할 수 있도록 서비스에 **모든** 권한이 필요 합니다. 또한 애플리케이션 설정에 대한 관리 권한을 가져야 하는 다른 SharePoint 사용자의 Windows 도메인 사용자 계정을 지정합니다.  
  
13. **확인**을 클릭합니다.  
  
14. 방금 만든 대상 응용 프로그램을 선택 하 고 아래쪽 화살표를 클릭 한 다음 **자격 증명 설정을 선택 합니다.**  
  
15. 자격 증명 **소유자**에서 자격 증명을 업데이트 하는 권한을 부여할 Windows 도메인 사용자 계정을 입력 합니다. 자격 증명은 데이터 새로 고침 작업에 사용 되 고 자격 증명 **소유자** 는 자격 증명을 수정할 수 있는 권한이 있습니다.  
  
16. **확인**을 클릭합니다.  
  
###  <a name="step-2-specify-the-unattended-account-in-powerpivot-server-configuration-pages"></a><a name="bkmk_specifyUA"></a>2 단계: PowerPivot 서버 구성 페이지에서 무인 계정 지정  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  PowerPivot 서비스 애플리케이션을 찾습니다. 유형을 기준으로 서비스 애플리케이션을 식별할 수 있습니다. PowerPivot 서비스 애플리케이션 유형은 **PowerPivot 서비스 애플리케이션**입니다.  
  
3.  PowerPivot 서비스 애플리케이션 이름을 클릭합니다. PowerPivot 관리 대시보드가 표시될 때까지 기다립니다.  
  
4.  작업의 오른쪽 위 모서리에서 **서비스 응용 프로그램 설정 구성**을 클릭 합니다.  
  
5.  데이터 새로 고침의 PowerPivot 무인 데이터 새로 고침 계정에 이전 단계에서 만든 대상 응용 프로그램 ID ( **PowerPivotDataRefresh**)를 입력 합니다.  
  
6.  **확인**을 클릭합니다.  
  
###  <a name="step-3-grant-contribute-permissions-to-the-account"></a><a name="bkmk_grant"></a>3 단계: 계정에 참가 권한 부여  
 PowerPivot 무인 데이터 새로 고침 계정을 사용하려면 먼저 해당 계정으로 사용할 PowerPivot 통합 문서에 대한 참가 권한을 계정에 할당해야 합니다. 이 권한 수준은 라이브러리에서 통합 문서를 열고 데이터를 새로 고친 후 다시 라이브러리에 저장하는 데 필요합니다.  
  
 사용 권한 할당은 사이트 모음 관리자가 수행하는 단계입니다. SharePoint 사용 권한은 루트 사이트 모음이나 개별 문서 및 항목을 포함하여 루트 사이트 모음 아래의 모든 수준에서 할당할 수 있습니다. 사용 권한 설정 방법은 사용 권한의 세분화 정도에 따라 달라집니다. 다음 단계에서는 사용 권한을 부여하는 한 가지 방법을 보여 줍니다.  
  
1.  SharePoint 사이트의 사이트 작업에서 **사이트 사용 권한**을 클릭 합니다.  
  
2.  **권한 부여**를 클릭합니다.  
  
3.  사용자 선택에서 PowerPivot 무인 계정으로 지정한 Windows 도메인 사용자 계정의 이름을 입력합니다. 이 이름은 보안 스토리지 서비스에서 대상 애플리케이션에 지정한 Windows 도메인 사용자 계정의 이름입니다.  
  
4.  권한 부여에서 사용자에 **게 직접 권한 부여**를 선택 합니다.  
  
5.  **참가**를 선택 하 고 **확인**을 클릭 합니다.  
  
###  <a name="step-4-grant-read-permissions-to-access-external-data-sources-used-in-data-refresh"></a><a name="bkmk_dbread"></a>4 단계: 데이터 새로 고침에 사용 되는 외부 데이터 원본에 액세스할 수 있는 읽기 권한 부여  
 PowerPivot 통합 문서로 데이터를 가져올 때 외부 데이터에 대한 연결은 현재 사용자의 ID를 데이터 원본에 연결하는 데 사용하는 가장된 연결이나 트러스트된 연결을 기반으로 하는 경우가 많습니다. 이러한 유형의 연결은 현재 사용자에게 자신이 가져오는 데이터를 읽을 수 있는 권한이 있는 경우에만 작동합니다.  
  
 데이터 새로 고침 시나리오에서는 데이터를 가져오는 데 사용된 것과 같은 연결 문자열이 데이터를 새로 고치는 데 다시 사용됩니다. 연결 문자열이 현재 사용자를 가정하는 경우(예를 들어 Integrated_Security=SSPI를 포함하는 문자열의 경우), PowerPivot 시스템 서비스에서는 PowerPivot 무인 데이터 새로 고침 계정의 사용자 ID를 현재 사용자로 전달합니다. 이 연결은 PowerPivot 무인 데이터 새로 고침 계정에 외부 데이터 원본에 대한 읽기 권한이 있는 경우에만 성공합니다.  
  
 따라서 PowerPivot 무인 데이터 새로 고침 계정에는 무인 계정에서 실행되는 모든 데이터 새로 고침 작업에 사용되는 모든 외부 데이터 원본에 대한 읽기 전용 권한을 부여해야 합니다.  
  
 조직에서 사용하는 데이터 원본의 관리자인 경우 로그인을 만들고 필요한 사용 권한을 할당할 수 있습니다. 그렇지 않은 경우에는 데이터 소유자에게 문의하여 계정 정보를 제공해야 합니다. PowerPivot 무인 데이터 새로 고침 계정에 매핑할 Windows 도메인 사용자 계정을 지정해야 합니다. 이는이 항목의 "(1 단계): 대상 응용 프로그램 만들기 및 자격 증명 설정"에서 지정한 계정입니다.  
  
###  <a name="step-5-verify-account-availability-in-data-refresh-configuration-pages"></a><a name="bkmk_verify"></a>5 단계: 데이터 새로 고침 구성 페이지에서 계정 가용성 확인  
  
1.  PowerPivot 데이터가 포함되어 있는 게시된 통합 문서에 대한 데이터 새로 고침 구성 페이지를 엽니다. 페이지를 여는 방법에 대 한 지침은 [데이터 새로 고침 예약 &#40;SharePoint용 PowerPivot&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)를 참조 하세요.  
  
2.  데이터 새로 고침 구성 페이지에서 **관리자가 구성한 데이터 새로 고침 계정 사용** 옵션이 설정 되어 있는지 확인 합니다.  
  
3.  **가능한 빨리 새로 고치십시오** . 확인란을 선택 하 고 **확인**을 클릭 합니다.  
  
4.  통합 문서가 포함 된 라이브러리에서 통합 문서를 선택 하 고 오른쪽에 표시 되는 아래쪽 화살표를 클릭 한 다음 **PowerPivot 데이터 새로 고침 관리**를 선택 합니다. 데이터 새로 고침 작업이 많은 데이터를 반환하는 경우 몇 분을 기다려야 할 수 있습니다.  
  
 오류가 발생 하는 경우 데이터 새로 고침 기록 페이지에서 **일정 구성** 을 클릭 하 여 다른 자격 증명을 시도할 수 있습니다. 또한 원래 통합 문서의 데이터 원본 연결 정보를 검사하여 데이터를 새로 고치는 동안 사용되는 연결 문자열을 확인해야 할 수 있습니다. 연결 문자열은 문제를 해결하는 데 사용할 수 있는 데이터베이스와 서버 위치에 대한 정보를 제공합니다.  
  
 문제 해결에 대 한 자세한 내용은 TechNet Wiki의 [PowerPivot 데이터 새로 고침 문제 해결](https://go.microsoft.com/fwlink/p/?LinkID=223279) 을 참조 하십시오.  
  
##  <a name="using-the-powerpivot-unattended-data-refresh-account"></a><a name="bkmk_use"></a>PowerPivot 무인 데이터 새로 고침 계정 사용  
 PowerPivot 무인 데이터 새로 고침 일정 예약 페이지의 세 가지 자격 증명 옵션 중 첫 번째 옵션만 무인 데이터 새로 고침 계정에 해당합니다. 데이터 새로 고침 일정을 설정할 때에는 이 옵션을 선택해야 합니다.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 PowerPivot 무인 데이터 새로 고침 계정에 액세스하는 데 세 번째 자격 증명 옵션(대상 애플리케이션 ID를 입력해야 함)을 사용하지 마십시오. 이 옵션의 경우 추가 가장 검사가 수행되므로 이 옵션을 PowerPivot 무인 데이터 새로 고침 계정(또는 개별 계정 유형에 기반한 임의의 대상 애플리케이션)에 사용하려고 하면 유효성 검사 오류가 발생합니다. 세 번째 옵션을 사용 하는 방법에 대 한 자세한 내용은 [PowerPivot 데이터 새로 고침을 위한 저장 된 자격 증명 구성 &#40;SharePoint용 PowerPivot&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)을 참조 하십시오.  
  
##  <a name="update-the-credentials-used-by-an-existing-powerpivot-unattended-data-refresh-account"></a><a name="bkmk_editUA"></a>기존 PowerPivot 무인 데이터 새로 고침 계정에서 사용 하는 자격 증명 업데이트  
 설치 중 또는 관리자를 통해 무인 데이터 새로 고침 계정이 이미 구성되어 있는 경우 해당 자격 증명이 저장된 대상 애플리케이션을 편집하여 사용자 이름이나 암호를 업데이트할 수 있습니다. 보안 저장소 서비스에서 자격 증명을 수정하면 이전에 PowerPivot 무인 데이터 새로 고침 계정과 관련되어 있던 원래 Windows ID가 표시되지 않습니다. 만료된 암호를 업데이트하거나 다른 계정을 지정할 경우 보안 스토리지 서비스에서 해당 대상 애플리케이션에 사용할 사용자 이름과 암호를 항상 다시 입력해야 합니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  **보안 저장소 서비스**를 클릭 합니다.  
  
3.  **PowerPivotDataRefresh**옆의 확인란을 선택 합니다.  
  
4.  자격 증명에서 **설정**을 클릭 합니다.  
  
5.  자격 증명 **소유자**에서 자격 증명을 업데이트 하는 권한을 부여할 Windows 도메인 사용자 계정을 입력 합니다. 자격 증명은 데이터 새로 고침 작업에 사용 되 고 자격 증명 **소유자** 는 자격 증명을 수정할 수 있는 권한이 있습니다.  
  
6.  사용자 이름에 무인 데이터 새로 고침 자격 증명의 일부가 될 Windows 도메인 사용자 계정을 입력합니다.  
  
7.  암호에 계정 암호를 입력한 다음 다시 입력하여 암호를 확인합니다.  
  
8.  **확인**을 클릭합니다.  
  
 암호만 변경하는 것이 아니라 계정 사용자 이름까지 변경하는 경우 외부 데이터 원본에 대한 읽기 권한 부여, PowerPivot 통합 문서를 업데이트할 수 있는 SharePoint 사용 권한 부여와 같은 추가 구성 단계를 추가해야 하는 경우가 대부분입니다. 자세한 내용은 PowerPivot 무인 데이터 새로 고침 계정 구성: [3 단계: 계정에 참가 권한 부여](#bkmk_grant)에서이 단계로 이동 하 고 나머지 모든 단계를 계속 진행 한 후 계정이 올바르게 구성 되었는지 확인 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 2010를 사용 하 여 PowerPivot 데이터 새로 고침](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [데이터 새로 고침 예약 &#40;SharePoint용 PowerPivot&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [PowerPivot 데이터 새로 고침](power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
