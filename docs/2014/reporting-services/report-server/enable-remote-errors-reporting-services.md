---
title: 원격 오류 활성화(Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- remote data source [Reporting Services]
- EnableRemoteError server property
ms.assetid: 5f05022b-d557-43e0-b50a-f5e2a1846b83
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e2d239dfc3d094f72d40ce6d020610fe1c0eabbc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103813"
---
# <a name="enable-remote-errors-reporting-services"></a>원격 오류 활성화(Reporting Services)
  원격 서버에서 발생되는 오류 조건에 대한 추가 정보를 반환하도록 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에 대한 서버 속성을 설정할 수 있습니다. 오류 메시지에 "이 오류에 대한 자세한 내용을 보려면 로컬 서버 컴퓨터의 보고서 서버를 탐색하거나 원격 오류를 활성화하십시오"라는 텍스트가 포함되어 있으면 문제 해결에 도움이 되는 추가 정보에 액세스할 수 있도록 `EnableRemoteErrors` 속성을 설정할 수 있습니다. 자세한 내용은 [온라인 설명서에서](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md) 보고서 서버 시스템 속성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
 **항목 내용**  
  
-   [SharePoint 모드에 대 한 원격 오류 사용](#bkmk_sharepoint)  
  
-   [SQL Server Management Studio를 통한 원격 오류 사용 (기본 모드)](#bkmk_mgtStudio)  
  
-   [스크립트를 통한 원격 오류 사용 (기본 모드)](#bkmk_script)  
  
-   [ConfigurationInfo 테이블 수정 (기본 모드)](#bkmk_ConfigurationInfo)  
  
##  <a name="bkmk_sharepoint"></a>SharePoint 모드에 대 한 원격 오류 사용  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에 대한 원격 오류 사용에는 두 가지 다른 프로시저가 있습니다. 서로 다른 두 보고서 서버 아키텍처에 따라 프로시저가 달라집니다. 
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 릴리스에서 도입된 새 SharePoint 서비스 기반 아키텍처는 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대해 구성될 수 있는 설정을 활용합니다. 이전 아키텍처는 단일 사이트 수준 설정을 활용합니다.  
  
#### <a name="enable-remote-errors-for-a-reporting-services-service-application"></a>Reporting Services 서비스 애플리케이션에 대한 원격 오류 사용  
  
1.  
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 새 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 함께 설치되는 SharePoint 모드 보고서 서버의 경우 서비스 애플리케이션 설정 **원격 오류 사용**을 설정합니다. 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대해 이 설정을 구성할 수 있습니다.  
  
2.  SharePoint 중앙 관리의 **응용 프로그램 관리** 그룹에서 **서비스 응용 프로그램 관리** 를 클릭 합니다.  
  
3.  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 찾아 해당 서비스 애플리케이션의 이름을 클릭합니다.  
  
4.  **시스템 설정**을 클릭합니다.  
  
5.  
  **보안** 섹션에서 **원격 오류 사용** 을 클릭합니다.  
  
6.  **확인**을 클릭합니다.  
  
#### <a name="enable-remote-errors-for-a-sharepoint-site"></a>SharePoint 사이트에 대한 원격 오류 사용  
  
1.  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이전의 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]버전과 함께 설치되는 SharePoint 모드 보고서 서버의 경우 사이트 설정 **로컬 모드에서 원격 오류 사용**을 설정합니다.  
  
2.  
  **사이트 작업** 에서 수정할 사이트의 **사이트 설정** 을 클릭합니다.  
  
3.  
  **Reporting Services** 그룹에서 **Reporting Services 사이트 설정** 을 클릭합니다.  
  
4.  
  **로컬 모드에서 원격 오류 사용**을 클릭합니다.  
  
5.  **확인을** 클릭 합니다.  
  
##  <a name="bkmk_mgtStudio"></a>SQL Server Management Studio를 통한 원격 오류 사용 (기본 모드)  
  
1.  Management Studio를 시작하여 보고서 서버 인스턴스에 연결합니다. 자세한 내용은 [온라인 설명서에서](../tools/connect-to-a-report-server-in-management-studio.md) Management Studio에서 보고서 서버에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
2.  보고서 서버 노드를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
3.  
  **고급** 을 클릭하여 속성 페이지를 엽니다. 자세한 내용은 [ 온라인 설명서에서 ](../tools/server-properties-advanced-page-reporting-services.md)서버 속성&#40;고급 페이지&#41; - Reporting Services[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조하세요.  
  
4.  에서 `EnableRemoteErrors`을 선택 `True`합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_script"></a>스크립트를 통한 원격 오류 사용 (기본 모드)  
  
1.  텍스트 파일을 만들고 다음 스크립트를 파일에 복사합니다.  
  
    ```  
    Public Sub Main()  
      Dim P As New [Property]()  
      P.Name = "EnableRemoteErrors"  
      P.Value = True  
      Dim Properties(0) As [Property]  
      Properties(0) = P  
      Try  
        rs.SetSystemProperties(Properties)  
        Console.WriteLine("Remote errors enabled.")  
      Catch SE As SoapException  
        Console.WriteLine(SE.Detail.OuterXml)  
      End Try  
    End Sub  
    ```  
  
2.  파일을 EnableRemoteErrors.rss로 저장합니다.  
  
3.  
  **시작**을 클릭하고 **실행**을 클릭한 다음 **cmd**를 입력하고 **확인** 을 클릭하여 명령 프롬프트 창을 엽니다.  
  
4.  방금 만든 .rss 파일이 포함된 디렉터리로 이동합니다.  
  
5.  다음 명령줄을 입력합니다. *servername* 은 서버의 실제 이름으로 바꿉니다.  
  
    ```  
    rs -i EnableRemoteErrors.rss -s http://servername/ReportServer  
    ```  
  
6.  자세한 내용은 [RS 유틸리티 &#40;SSRS](../tools/rs-exe-utility-ssrs.md) 를 참조 하세요&#41;  
  
##  <a name="bkmk_ConfigurationInfo"></a>ConfigurationInfo 테이블 수정 (기본 모드)  
  
1.  > [!NOTE]  
    >  보고서 서버 데이터베이스의 **Configurationinfo** 테이블을로 `EnableRemoteErrors` `True`설정 하 여 편집할 수 있지만 보고서 서버가 현재 사용 중인 경우에는 SQL Server Management Studio 또는 스크립트를 사용 하 여 설정을 수정 해야 합니다. 데이터베이스에서 이 설정을 수정하는 경우 변경 내용을 적용하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 다시 시작해야 합니다.  
  
  
