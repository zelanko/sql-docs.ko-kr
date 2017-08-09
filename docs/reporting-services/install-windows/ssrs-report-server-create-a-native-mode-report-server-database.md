---
title: "기본 모드 보고서 서버 데이터베이스 (SSRS 구성 관리자) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], databases
- databases [Reporting Services], creating
ms.assetid: 81b9f4ad-800b-4688-8b47-a5a83dc8ff10
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1458fe51bc43c24904be30c5484f8829f8b45ebc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---

# <a name="create-a-native-mode-report-server-database"></a>기본 모드 보고서 서버 데이터베이스 만들기

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

기본 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 내부 저장소로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 사용합니다. 이 데이터베이스는 필수 항목이며 게시된 보고서, 모델, 공유 데이터 원본, 세션 데이터, 리소스 및 서버 메타데이터를 저장하는 데 사용됩니다.  

보고서 서버 데이터베이스를 만들거나 연결 문자열 또는 자격 증명을 변경하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자의 데이터베이스 페이지에 있는 옵션을 사용하십시오.  
  
## <a name="when-to-create-or-configure-the-report-server-databases"></a>보고서 서버 데이터베이스를 만들거나 구성하는 경우  
 보고서 서버를 파일만 모드에서 설치한 경우 보고서 서버 데이터베이스를 만들고 구성해야 합니다.  
  
 기본 모드용 기본 구성으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치한 경우 보고서 서버 인스턴스가 설치되면 보고서 서버 데이터베이스가 자동으로 만들어지고 구성됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 설치 프로그램이 자동으로 구성한 설정을 확인하거나 수정할 수 있습니다.  
  
##  <a name="rsdbrequirements"></a> 시작하기 전에  
 보고서 서버 데이터베이스를 만들거나 구성하려면 여러 단계를 수행해야 합니다. 보고서 서버 데이터베이스를 만들기 전에 다음 항목을 지정하는 방법을 고려해야 합니다.  
  
 **데이터베이스 서버 선택**  
 [보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md) 항목에서 지원되는 버전 및 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 지원되는 버전을 검토합니다.  
  
 **TCP/IP 연결 설정**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대해 TCP/IP 연결을 설정하십시오. 일부 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 버전은 기본적으로 TCP/IP 연결을 설정하지 않습니다. 지침은 이 항목에 설명되어 있습니다.  
  
 **다음 포트 열기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
 원격 서버에 대해 방화벽 소프트웨어를 사용하고 있는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 수신할 포트를 열어야 합니다.  
  
 **보고서 서버 자격 증명 결정**  
 보고서 서버가 보고서 서버 데이터베이스에 연결되는 방식을 결정하십시오. 자격 증명 유형에는 도메인 사용자 계정, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 계정 또는 보고서 서버 서비스 계정이 있습니다.  
  
 이러한 자격 증명은 RSReportServer.config 파일에 암호화되어 저장됩니다. 보고서 서버는 보고서 서버 데이터베이스에 대한 지속적인 연결에 이 자격 증명을 사용합니다. Windows 사용자 계정 또는 데이터베이스 사용자 계정을 사용하려는 경우 이미 존재하는 계정을 지정해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 로그인을 만들고 필요한 사용 권한을 설정하지만 계정을 만들지는 않습니다. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)의 지원되는 버전을 검토합니다.  
  
 **보고서 서버 언어 결정**  
 보고서 서버에 대해 지정할 언어를 선택하십시오. 사용자가 브라우저의 다른 언어 버전을 사용하여 서버에 연결할 경우 미리 정의된 역할 이름, 설명 및 내 보고서 폴더는 다른 언어로 표시되지 않습니다.  
  
 **데이터베이스를 만들고 제공할 자격 증명 확인**  
 계정 자격 증명이 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 데이터베이스를 만들 수 있는 권한을 가지고 있는지 확인합니다. 이러한 자격 증명은 보고서 서버 데이터베이스와 **RSExecRole**을 만들기 위한 일회성 연결에 사용됩니다. 로그인이 없는 경우 보고서 서버에서 데이터베이스에 연결할 때 사용하는 계정에 대해 데이터베이스 사용자 로그인이 만들어집니다. 현재 로그인한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정으로 연결하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인을 입력할 수 있습니다.  
  
### <a name="to-enable-access-to-a-remote-report-server-database"></a>원격 보고서 서버 데이터베이스에 대한 액세스를 허용하려면  
  
1.  원격 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 사용하는 경우 데이터베이스 서버로 로그온하여 TCP/IP 연결을 확인하거나 설정합니다.  
  
2.  **시작**, **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
3.  **SQL Server 네트워크 구성**을 엽니다.  
  
4.  데이터베이스 인스턴스를 선택합니다.  
  
5.  **TCP/IP** 를 마우스 오른쪽 단추로 클릭한 다음 **사용**을 선택합니다.  
  
6.  서비스를 다시 시작합니다.  
  
7.  방화벽 소프트웨어를 연 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 수신할 포트를 엽니다. 기본 인스턴스의 경우 이는 일반적으로 TCP/IP 연결용 포트 1433입니다. 자세한 내용은 [온라인 설명서의](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) 데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
### <a name="to-create-a-local-report-server-database"></a>로컬 보고서 서버 데이터베이스를 만들려면  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작한 다음 데이터베이스를 만들려는 보고서 서버 인스턴스에 연결합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)의 지원되는 버전을 검토합니다.  
  
2.  데이터베이스 페이지에서 **데이터베이스 변경**을 선택합니다.  
  
3.  **새 보고서 서버 데이터베이스 만들기**를 선택한 후 **다음**을 선택합니다.  
  
4.  보고서 서버 데이터베이스를 만들고 호스팅하는 데 사용할 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
  
    1.  사용할 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스를 입력합니다. 사용 가능한 경우 기본 인스턴스로 실행되는 로컬 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 표시됩니다. 그렇지 않으면 사용할 서버와 인스턴스를 입력해야 합니다. 이 형식으로 지정 된 명명 된 인스턴스: \<서버 이름 >\\< instancename\>합니다.  
  
    2.  보고서 서버 데이터베이스를 만들기 위해 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 대한 일회성 연결에 사용되는 자격 증명을 입력합니다. 이 자격 증명이 사용되는 방식은 이 항목에 포함된 [시작하기 전에](#rsdbrequirements) 를 참조하십시오.  
  
    3.  **연결 테스트** 를 클릭하여 서버 연결의 유효성을 검증합니다.  
  
    4.  **다음**을 선택합니다.  
  
5.  데이터베이스를 만드는 데 사용된 속성을 지정합니다. 이 속성이 사용되는 방식은 이 항목에 포함된 [시작하기 전에](#rsdbrequirements) 를 참조하십시오.  
  
    1.  보고서 서버 데이터베이스의 이름을 입력합니다. 주 데이터베이스와 함께 임시 데이터베이스가 생성됩니다. 데이터베이스가 사용되는 방식을 기억하는 데 도움이 되도록 설명이 포함된 이름을 사용하십시오. 지정하는 이름은 데이터베이스의 수명이 유지되는 동안 사용됩니다. 보고서 서버 데이터베이스를 만든 후에는 이름을 바꿀 수 없습니다.  
  
    2.  역할 정의 및 내 보고서를 표시하는 데 사용할 언어를 선택합니다.  
  
    3.  보고서 서버 모드는 항상 **기본**으로 설정합니다.  
  
    4.  **다음**을 선택합니다.  
  
6.  보고서 서버가 보고서 서버 데이터베이스에 연결할 때 사용할 자격 증명을 지정합니다.  
  
    1.  인증 유형을 지정합니다.  
  
         이미 정의된 **** 데이터베이스 로그인을 사용하여 연결하려면 데이터베이스 자격 증명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 선택합니다. 보고서 서버가 다른 도메인이나 트러스트되지 않은 도메인에 있는 컴퓨터 또는 방화벽 뒤에 있는 컴퓨터에 있는 경우 데이터베이스 자격 증명을 사용하는 것이 좋습니다.  
  
         컴퓨터와 보고서 서버에 대한 로그온 권한을 가진 최소 권한 도메인 사용자 계정이 있는 경우에는 **Windows 자격 증명** 을 선택합니다.  
  
         서비스 계정을 사용하여 보고서 서버에 연결하려면 **서비스 자격 증명** 을 선택합니다. 이 옵션을 사용하면 통합 보안을 사용하여 서버에 연결되지만 자격 증명이 암호화되거나 저장되지는 않습니다.  
  
    2.  **다음**을 선택합니다.  
  
7.  요약 페이지에서 설정이 올바른지 확인한 후 **다음**을 클릭합니다.  
  
8.  보고서 서버 URL 페이지 또는 보고서 관리자 URL 페이지의 URL을 선택하여 연결을 확인합니다. URL은 이 테스트가 작동하는 순서로 정의되어야 합니다. 보고서 서버 데이터베이스 연결이 유효한 경우 보고서 서버 폴더 계층이나 보고서 관리자가 브라우저 창에 표시됩니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) Reporting Services 설치 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  

## <a name="change-database-credentials"></a>데이터베이스 자격 증명 변경

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 보고서 서버 데이터베이스에 연결할 때 보고서 서버에서 사용하는 계정을 다시 구성하는 단계를 안내하는 자격 증명 변경 마법사를 제공합니다. 자격 증명을 변경할 때 구성 관리자는 보고서 서버에서 현재 사용 중인 보고서 서버 데이터베이스의 데이터베이스 서버에 대한 모든 사용 권한과 데이터베이스 로그인 정보를 업데이트합니다. 

1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작한 다음 데이터베이스를 만들려는 보고서 서버 인스턴스에 연결합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)의 지원되는 버전을 검토합니다.  
  
2.  데이터베이스 페이지에서 **자격 증명 변경**을 선택합니다. 

3.  보고서 서버 데이터베이스를 만들고 호스팅하는 데 사용할 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
  
    1.  보고서 서버 데이터베이스를 만들기 위해 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 대한 일회성 연결에 사용되는 자격 증명을 입력합니다. 이 자격 증명이 사용되는 방식은 이 항목에 포함된 [시작하기 전에](#rsdbrequirements) 를 참조하십시오.  
  
    2.  **연결 테스트** 를 클릭하여 서버 연결의 유효성을 검증합니다.  
  
    3.  **다음**을 선택합니다.  

4.  보고서 서버가 보고서 서버 데이터베이스에 연결할 때 사용할 자격 증명을 지정합니다.  
  
    1.  인증 유형을 지정합니다.  
  
         이미 정의된 **** 데이터베이스 로그인을 사용하여 연결하려면 데이터베이스 자격 증명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 선택합니다. 보고서 서버가 다른 도메인이나 트러스트되지 않은 도메인에 있는 컴퓨터 또는 방화벽 뒤에 있는 컴퓨터에 있는 경우 데이터베이스 자격 증명을 사용하는 것이 좋습니다.  
  
         컴퓨터와 보고서 서버에 대한 로그온 권한을 가진 최소 권한 도메인 사용자 계정이 있는 경우에는 **Windows 자격 증명** 을 선택합니다.  
  
         서비스 계정을 사용하여 보고서 서버에 연결하려면 **서비스 자격 증명** 을 선택합니다. 이 옵션을 사용하면 통합 보안을 사용하여 서버에 연결되지만 자격 증명이 암호화되거나 저장되지는 않습니다.  
  
    2.  **다음**을 선택합니다. 

5. 설정을 검토하고 **다음**을 선택합니다.

6. 변경 후 **마침**을 선택합니다.

## <a name="next-steps"></a>다음 단계

[보고서 서버 데이터베이스 연결 구성](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[Reporting Services 구성 관리자](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
