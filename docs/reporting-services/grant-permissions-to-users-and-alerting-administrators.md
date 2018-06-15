---
title: 사용자 및 경고 관리자에게 사용 권한 부여 | Microsoft Docs
ms.custom: ''
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 136406ea820f89ff52df5921511227af80178054
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33016800"
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>사용자 및 경고 담당자에게 권한 부여

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

사용자 및 경고 담당자는 SharePoint 권한을 부여 받아야 경로를 만들고, 편집하고, 삭제하고 볼 수 있습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 알림 기능을 사용하는 데에는 특별한 권한이 필요 없이 기본 제공 SharePoint 권한을 사용합니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

**정보 근로자**- 경고 만들기 및 항목 보기 SharePoint 권한이 있어야 합니다. 디자인, 참가, 읽기, 보기만 등의 기본 제공 SharePoint 권한 수준은 경고 만들기 및 항목 보기 SharePoint 권한을 포함합니다. 알림을 만들고 편집하며 실행하고 보는 사용자를 지원하는 데 필요한 권한이 있으면 사용자 지정 권한 수준을 만들 수도 있습니다.

**경고 담당자**— 경고 관리 SharePoint 권한이 있어야 합니다. 기본적으로 팀 사이트 사이트 템플릿을 사용하여 만든 사이트에 대해서는 모든 권한 수준만 이 권한을 포함합니다. 다른 사이트 템플릿을 사용하는 경우 기본 SharePoint 그룹의 다른 목록이 표시됩니다. 기본 제공 권한 수준 중 하나에 경고 관리 권한을 추가할 수 있습니다. 또는 데이터 경고를 보고 삭제하는 경고 담당자를 지원하는 데 필요한 권한이 있으면 사용자 지정 권한 수준을 만들 수 있습니다.

SharePoint 권한에 대한 자세한 내용은 [사용자 권한 및 권한 수준(SharePoint Server 2010)](http://technet.microsoft.com/library/cc721640.aspx)을 참조하세요.

## <a name="grant-permissions"></a>사용 권한 부여
  
1.  사용 권한을 부여할 SharePoint 사이트로 이동합니다.  
  
2.  도구 모음에서 **사이트 작업** 을 클릭한 후 **사이트 사용 권한**을 클릭합니다.  
  
     이 옵션이 나타나지 않으면 다른 사람에게 권한을 부여할 권한이 없는 것입니다.  
  
3.  **사용 권한 부여**를 클릭합니다.  
  
4.  **사용자/그룹**에서 권한을 부여할 대상의 사용자 이름, 그룹 이름 또는 메일 주소를 입력합니다.  
  
5.  **SharePoint 그룹에 사용자 추가** 또는 **사용자에게 사용 권한 직접 부여** 옵션을 선택합니다. **SharePoint 그룹에 사용자 추가** 를 선택했는지, 아니면 **사용자에게 사용 권한 직접 부여** 를 선택했는지에 따라 다음 중 하나를 수행합니다.  
  
    -   **SharePoint 그룹에 사용자 추가**를 선택한 경우 드롭다운 목록에서 권한 수준을 선택합니다.  
  
    -   **사용자에게 사용 권한 직접 부여**를 선택한 경우 권한 수준을 선택합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

## <a name="see-also"></a>참고 항목

[SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
[Reporting Services 데이터 경고](../reporting-services/reporting-services-data-alerts.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
