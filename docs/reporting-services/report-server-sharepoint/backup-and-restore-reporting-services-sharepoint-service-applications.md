---
title: Reporting Services SharePoint 서비스 애플리케이션 백업 및 복원 | Microsoft Docs
description: SharePoint 중앙 관리 또는 PowerShell을 사용하여 SQL Server Reporting Services 서비스 애플리케이션을 백업하고 복원하는 방법을 알아봅니다.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: 559b88b776c92abfd98929f5b73cabb04a7f6d80
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474524"
---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Reporting Services SharePoint 서비스 애플리케이션 백업 및 복원

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

이 항목에서는 SharePoint 중앙 관리 또는 PowerShell을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 백업하고 복원하는 방법에 대해 설명합니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

## <a name="before-you-begin"></a>시작하기 전에

### <a name="limitations-and-restrictions"></a>제한 사항

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션은 SharePoint 백업 및 복원 기능을 사용하여 부분적으로 백업 및 복원할 수 있습니다. **추가 단계를 수행해야 하며** 단계는 이 항목에 설명되어 있습니다. 현재는 백업 프로세스를 진행해도 **데이터베이스에 대한 Windows 인증 또는 UEA(무인 실행 계정)를 위한 암호화 키 및 자격 증명이 백업되지** 않습니다[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

### <a name="recommendations"></a>권장 사항
  
-   SharePoint 백업을 시작하기 전에 암호화 키를 백업합니다. 암호화 키를 백업하지 않으면 서비스 애플리케이션을 복원한 후 암호화된 데이터에 액세스할 수 없습니다. 이 경우 암호화된 데이터를 삭제해야 합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 데이터베이스 액세스를 위해 UEA 또는 Windows 인증이 사용되고 있는지 확인합니다. 둘 중 하나가 사용되고 있는 경우 복원 프로세스 후에 서비스 애플리케이션을 올바르게 구성할 수 있도록 적절한 자격 증명이 무엇인지 확인합니다.  
  
-   SharePoint 백업 로그가 백업 파일과 동일한 폴더에 생성되어 있는지 검토합니다. 이 파일의 이름은 일반적으로 **spbackup.log** 입니다.  
  
## <a name="back-up-the-service-application"></a>서비스 애플리케이션 백업

 다음 단계를 순서대로 수행하세요.  
  
1.  암호화 키 백업  
  
2.  서비스 애플리케이션 백업  
  
3.  서비스 애플리케이션에 데이터베이스 액세스를 위해 UEA 또는 Windows 인증이 사용되고 있는지 확인합니다. 둘 중 하나가 사용되고 있는 경우 복원 후에 서비스 애플리케이션을 구성하는 데 사용할 수 있도록 자격 증명을 기록해 둡니다.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>SharePoint 중앙 관리를 사용하여 암호화 키 백업

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 암호화 키 백업에 대한 자세한 내용은 [Reporting Services SharePoint 서비스 애플리케이션 관리](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)의 "암호화 키" 섹션을 참조하세요.  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>SharePoint 중앙 관리를 사용하여 서비스 애플리케이션 백업

서비스 애플리케이션을 백업하려면 다음 단계를 수행하세요.  
  
1.  SharePoint 중앙 관리의 **백업 및 복원** 그룹에서 **백업 실행** 을 선택합니다.  
  
2.  **공유 서비스** 노드에서 **공유 서비스 애플리케이션** 을 확장하고 서비스 애플리케이션을 선택합니다. 유형은 **SQL Server Reporting Services 서비스 애플리케이션** 입니다.  
  
3.  **다음** 을 선택합니다.  
  
4.  **백업 위치:** 에 대한 경로를 입력하고 **백업 시작** 을 선택합니다.  
  
5.  위 프로세스를 반복하되 서비스 애플리케이션을 선택하는 대신 **공유 서비스 프록시** 노드를 확장하고 서비스 애플리케이션 프록시를 선택합니다. 유형은 **SQL Server Reporting Services 서비스 애플리케이션 프록시** 입니다.  
  
 자세한 내용은 SharePoint 설명서의 다음 항목을 참조하세요.  
  
 [SharePoint 설명서의 서비스 애플리케이션 백업(SharePoint Foundation 2010)](/previous-versions/office/sharepoint-foundation-2010/ee748601(v=office.14))  
  
 [서비스 애플리케이션 백업(SharePoint Server 2010)](/SharePoint/administration/back-up-a-service-application)  
  
### <a name="verify-execution-account-and-database-authentication"></a>실행 계정 및 데이터베이스 인증 확인

 **실행 계정:** 서비스 애플리케이션에 실행 계정이 사용되고 있는지 확인하려면  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리** 를 선택합니다.  
  
2.  서비스 애플리케이션의 이름을 선택한 다음 SharePoint 리본에서 **관리** 를 선택합니다.  
  
3.  **실행 계정** 을 선택합니다.  
  
4.  실행 계정이 구성된 경우 서비스 애플리케이션 백업을 복원할 때 자격 증명을 알아야 합니다. 올바른 자격 증명을 알 때까지 백업 및 복원 절차를 진행하지 마세요.  
  
 **데이터베이스 인증:** 서비스 애플리케이션에 데이터베이스 인증을 위해 Windows 인증이 사용되고 있는지 확인하려면  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리** 를 선택합니다.  
  
2.  서비스 애플리케이션의 이름을 선택한 다음 SharePoint 리본에서 **속성** 을 선택합니다.  
  
3.  **Reporting Services(SSRS) 서비스 데이터베이스** 섹션을 검토합니다.  
  
4.  Windows 인증이 구성된 경우 복원 후 서비스 애플리케이션을 구성할 수 있도록 자격 증명을 알아야 합니다. 올바른 자격 증명을 알 때까지 백업 및 복원 절차를 진행하지 마세요.  
  
## <a name="restore-the-service-application"></a>서비스 애플리케이션을 복원합니다.

 다음 단계를 순서대로 수행하세요.  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 복원합니다.  
  
2.  암호화 키를 복원합니다.  
  
3.  서비스 애플리케이션에 데이터베이스 액세스를 위해 실행 계정 또는 Windows 인증이 사용되고 있었던 경우 자격 증명을 구성합니다.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>SharePoint 중앙 관리를 사용하여 서비스 애플리케이션 복원
  
1.  SharePoint 중앙 관리의 **백업 및 복원** 그룹에서 **백업에서 복원** 을 선택합니다.  
  
2.  **백업 디렉터리 위치** 상자에서 백업 파일에 대한 경로를 입력하고 **새로 고침** 을 선택합니다.  
  
3.  **최상위 구성 요소** 목록에서 서비스 애플리케이션 백업을 선택하고 **다음** 을 선택합니다.  
  
4.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션을 선택하고 **다음** 을 선택합니다.  
  
5.  **로그인 이름 및 암호** 섹션에 로그인 이름의 암호를 입력합니다. 로그인 이름 입력란은 백업 전에 서비스 애플리케이션에 사용되던 로그인으로 채워야 합니다.  
  
6.  **복원 시작** 을 선택합니다.  
  
7.  위 프로세스를 반복하되 서비스 애플리케이션을 복원하는 대신 **공유 서비스** 노드와 **공유 서비스 애플리케이션** 노드를 차례로 확장합니다.  
  
 자세한 내용은 SharePoint 설명서의 다음 항목을 참조하세요.  
  
 [서비스 애플리케이션 복원(SharePoint Foundation 2010)](/previous-versions/office/sharepoint-foundation-2010/ee748615(v=office.14))  
  
 [서비스 애플리케이션 복원(SharePoint Server 2010)](/SharePoint/administration/restore-a-service-application)  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>SharePoint 중앙 관리를 사용하여 암호화 키 복원

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 암호화 키 복원에 대한 자세한 내용은 [Reporting Services SharePoint 서비스 애플리케이션 관리](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)의 "암호화 키" 섹션을 참조하세요.  

### <a name="configure-the-execution-account-and-database-authentication"></a>실행 계정 및 데이터베이스 인증 구성

 **실행 계정:** 서비스 애플리케이션에 실행 계정이 사용되고 있었던 경우 다음 단계를 수행하여 구성합니다.  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리** 를 선택합니다.  
  
2.  서비스 애플리케이션의 이름을 선택한 다음 SharePoint 리본에서 **관리** 를 선택합니다.  
  
3.  **실행 계정** 을 선택합니다.  
  
4.  계정 및 암호를 입력하고 **실행 계정 지정** 입력란을 선택합니다.  
  
5.  **확인** 을 선택합니다.  
  
 **데이터베이스 인증:** 서비스 애플리케이션에 데이터베이스 인증을 위해 Windows 인증이 사용되고 있었던 경우 다음 단계를 수행합니다.  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리** 를 선택합니다.  
  
2.  서비스 애플리케이션의 이름을 선택한 다음 SharePoint 리본에서 **속성** 을 선택합니다.  
  
3.  **Reporting Services(SSRS) 서비스 데이터베이스** 섹션을 검토합니다.  
  
4.  **Windows 인증** 을 선택합니다.  
  
5.  계정 및 암호를 입력합니다. 해당되는 경우 **Windows 자격 증명으로 사용** 을 선택합니다.  
  
6.  **확인** 을 선택합니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)