---
title: Reporting Services 서비스 응용 프로그램에 대한 전자 메일 구성 | Microsoft Docs
ms.date: 05/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 26c28f65737fe989b416078e609f7742cfcf07b1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410370"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application"></a>Reporting Services 서비스 응용 프로그램에 대한 전자 메일 구성

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고는 메일 메시지로 경고를 보냅니다. 전자 메일을 보내기 위해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 구성하고 서비스 응용 프로그램을 위한 전자 메일 배달 확장 프로그램을 수정해야 할 수 있습니다. 또한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가입 기능을 위해 전자 메일 배달 확장 프로그램을 사용할 계획인 경우에도 전자 메일 설정이 필요합니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.
  
### <a name="to-configure-e-mail-for-the-shared-service"></a>공유 서비스에 대한 전자 메일 구성 방법  
  
1.  SharePoint 중앙 관리에서 **응용 프로그램 관리**를 클릭합니다.  
  
2.  **서비스 응용 프로그램** 그룹에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
3.  **이름** 목록에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 이름을 클릭합니다.  
  
4.  **Reporting Services 응용 프로그램 관리** 페이지에서 **메일 설정** 을 클릭합니다.  
  
5.  **SMTP 서버 사용**을 선택합니다.  
  
6.  **아웃바운드 SMTP 서버** 상자에 SMTP 서버 이름을 입력합니다.  
  
7.  **보낸 사람 주소** 상자에서 메일 주소를 입력합니다.  
  
     이 주소는 모든 경고 전자 메일 메시지의 받는 사람입니다.  
  
     **보낸 사람 주소** 에 지정한 사용자 계정은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 응용 프로그램 풀을 구성할 때 지정한 관리 계정이어야 합니다. 권한이 있는 경우 SharePoint 중앙 관리의 서비스 계정 페이지에서 기존 관리 계정 목록을 볼 수 있습니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="ntlm-authentication"></a>NTLM 인증  
  
1.  해당 전자 메일 환경에서 NTLM 인증이 필요하고 익명 액세스가 허용되지 않는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 대해 전자 메일 배달 확장 프로그램 구성을 수정해야 합니다. 예를 들어 **구독 관리** 페이지: 구독의 **마지막 결과** 에 다음과 같은 메시지가 표시되는 경우입니다.  
  
    -   메일 전송 실패: SMTP 서버에 보안 연결이 필요하거나 클라이언트가 인증되지 않았습니다. 서버 응답: 5.7.1 클라이언트가 인증되지 않았습니다. 메일이 다시 전송되지 않습니다.  
  
     "2" 값을 사용하도록 **SMTP 인증**을 변경합니다. 이 값은 사용자 인터페이스에서 변경할 수 없습니다. 다음 PowerShell 스크립트 예에서 "SSRS_TESTAPPLICATION" 서비스 애플리케이션에 대해 보고서 서버 이메일 배달 확장 프로그램의 전체 구성을 업데이트합니다. 또한 예를 들어 "보낸 사람" 주소와 같이 스크립트에 나열된 일부 노드는 사용자 인터페이스에서 설정할 수 있습니다.  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
    $emailXml = [xml]$emailCfg   
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = "your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = "your FROM email address"  
    Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  서비스 응용 프로그램 이름을 확인해야 하는 경우 **Get-SPRSServiceApplication cmdlet**을 실행합니다.  
  
    ```  
    get-sprsserviceapplication  
    ```  
  
3.  다음 예제에서 "SSRS_TESTAPPLICATION" 서비스 애플리케이션에 대해 이메일 확장 프로그램의 현재 값으로 되돌립니다.  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
    ```  
  
4.  다음 예제에서 "SSRS_TESTAPPLICATION" 서비스 애플리케이션에 대해 이메일 확장 프로그램의 현재 값을 가진 "emailconfig.txt"라는 새 파일을 생성합니다.  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml | out-file c:\emailconfig.txt  
    ```  
  
  
추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
