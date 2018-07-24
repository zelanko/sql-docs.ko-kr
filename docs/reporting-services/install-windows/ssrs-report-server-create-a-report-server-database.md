---
title: 보고서 서버 데이터베이스 만들기(SSRS 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8cee752f2168929723dae86cd0da774cb02518bd
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983585"
---
# <a name="create-a-report-server-database"></a>보고서 서버 데이터베이스 만들기

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **기본 모드** 에서는 보고서 서버 메타데이터 및 개체를 저장하기 위해 두 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스를 사용합니다. 한 데이터베이스는 주 저장소로 사용되고 다른 데이터베이스는 임시 데이터를 저장하는 데 사용됩니다. 데이터베이스는 함께 생성되며 이름별로 바인딩됩니다. 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용하면 데이터베이스 이름은 각각 **reportserver** 와 **reportservertempdb**입니다. 이 두 데이터베이스는 "보고서 서버 데이터베이스" 또는 "보고서 서버 카탈로그"로 통칭됩니다.

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **SharePoint 모드** 에는 데이터 경고 메타데이터에 사용되는 세 번째 데이터베이스를 포함합니다. 세 개의 데이터베이스가 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 대해 만들어지고 데이터베이스 이름에는 기본적으로 서비스 응용 프로그램을 나타내는 GUID가 포함됩니다. 다음은 세 가지 SharePoint 모드 데이터베이스의 이름 예입니다.

-   ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
>  보고서 서버 데이터베이스에 대해 쿼리를 실행하는 응용 프로그램을 작성하지 마십시오. 보고서 서버 데이터베이스는 공용 스키마가 아닙니다. 현재 릴리스의 테이블 구조는 다음 릴리스에서 변경될 수 있습니다. 보고서 서버 데이터베이스에 액세스해야 하는 응용 프로그램을 작성하는 경우에는 항상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API를 사용하여 보고서 서버 데이터베이스에 액세스하십시오.  
>   
>  이에 대한 예외는 실행 로그 뷰입니다. 자세한 내용은 [보고서 서버 ExecutionLog 및 ExecutionLog3 뷰](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)를 참조하세요.  
  
## <a name="ways-to-create-the-report-server-database"></a>보고서 서버 데이터베이스를 만드는 방법  
 **기본 모드:** 다음과 같은 방법으로 기본 모드 보고서 서버 데이터베이스를 만들 수 있습니다.  
  
-   자동으로: 기본 구성 설치 옵션을 선택하는 경우 SQL Server 설치 마법사를 사용합니다. SQL Server 설치 마법사에서 이 옵션은 보고서 서버 설치 옵션 페이지의 **설치 및 구성** 입니다. **설치만** 옵션을 선택한 경우 Reporting Services 구성 관리자를 사용하여 데이터베이스를 만들어야 합니다.  
  
-   수동으로: [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용합니다. 원격 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 을 사용하여 데이터베이스를 호스팅하는 경우 보고서 서버 데이터베이스를 수동으로 만들어야 합니다. 자세한 내용은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.  
  
 **SharePoint 모드:** 보고서 서버 설치 옵션 페이지에는 **설치 전용**인 SharePoint 모드 옵션 하나만 포함됩니다. 이 옵션은 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 파일 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스를 설치합니다. 다음 단계에는 다음 방법 중 하나를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 하나 이상 만듭니다.  
  
-   SharePoint 중앙 관리에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 만듭니다. 자세한 내용은 [Step 3: Create a Reporting Services Service Application](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication)의 “서비스/응용 프로그램” 단원을 참조하십시오.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] PowerShell cmdlet을 사용하여 서비스 응용 프로그램 및 보고서 서버 데이터베이스를 만듭니다. 자세한 내용은 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)항목에서 서비스 응용 프로그램 만들기 예제를 참조하세요.  
  
## <a name="database-server-version-requirements"></a>데이터베이스 서버 버전 요구 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 보고서 서버 데이터베이스를 호스팅하는 데 사용됩니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스는 로컬 또는 원격 인스턴스일 수 있습니다. 다음은 보고서 서버 데이터베이스를 호스팅하기 위해 사용할 수 있는 지원되는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 버전입니다.  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 원격 컴퓨터에 보고서 서버 데이터베이스를 만들려면 네트워크 액세스 권한이 있는 서비스 계정 또는 도메인 사용자 계정을 사용하도록 연결을 구성해야 합니다. 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용하려는 경우 보고서 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 사용해야 하는 자격 증명을 주의해서 선택하십시오. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)의 지원되는 버전을 검토합니다.  
  
> [!IMPORTANT]  
>  보고서 서버 데이터베이스를 호스팅하는 보고서 서버와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 서로 다른 도메인에 있을 수 있습니다. 인터넷 배포의 경우 방화벽 뒤에 있는 서버를 사용하는 것이 일반적입니다. 보고서 서버를 인터넷 액세스용으로 구성하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명을 사용하여 방화벽 뒤에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하고 IPSEC을 사용하여 연결 보안을 설정합니다.  
  
## <a name="database-server-edition-requirements"></a>데이터베이스 서버 에디션 요구 사항  
 보고서 서버 데이터베이스를 만들 때 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전은 데이터베이스 호스팅에 사용할 수 없습니다. 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)의 "보고서 서버 데이터베이스 서버 버전 요구 사항" 섹션을 참조하세요.  

## <a name="next-steps"></a>다음 단계

[Reporting Services 구성 관리자](http://msdn.microsoft.com/63519ef4-e68a-42fb-9cf7-31228ea4e434)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
