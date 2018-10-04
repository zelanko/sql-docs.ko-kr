---
title: 서버에 연결(로그인 페이지) Reporting Services | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7369e9d37e5f706786410f8e171c89c6c38287d2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108713"
---
# <a name="connect-to-server-login-page-reporting-services"></a>서버에 연결(로그인 페이지) Reporting Services
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에 연결할 때 이 탭을 사용하여 다음 옵션을 확인하거나 지정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **서버 유형**  
 개체 탐색기에서 서버를 등록할 때 연결할 서버 유형을 [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services 또는 Integration Services 중에서 선택합니다. 대화 상자의 나머지 부분에는 선택한 서버 유형에 적용되는 옵션만 표시됩니다. 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버 구성 요소에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 등록된 서버 도구 모음에서 [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services 또는 Integration Services를 선택합니다.  
  
 **서버 이름**  
 연결하려는 보고서 서버 인스턴스의 서버 모드에 따라 입력해야 하는 값이 결정됩니다.  
  
 기본 모드로 실행되는 보고서 서버의 경우 연결할 보고서 서버 인스턴스를 지정합니다. 기본 인스턴스를 사용하는 경우 서버 이름은 대개 컴퓨터 이름입니다. 명명된 된 인스턴스를 설치한 경우이 형식으로 서버 이름에 인스턴스 이름을 추가 합니다. \<서버 이름 >\\< n a m e\>합니다. Reporting Services는 백슬래시 문자를 사용하여 인스턴스 이름을 구분합니다.  
  
 SharePoint 통합 모드로 실행되는 보고서 서버의 경우 SharePoint 사이트를 지정해야 합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]와 통합된 사이트 컬렉션에 있는 아무 사이트나 지정할 수 있습니다. URL을 지정할 때는 HTTP 또는 HTTPS 접두사를 포함해야 합니다. Management Studio에서 보고서 서버 인스턴스에 연결하려면 SharePoint에 액세스할 수 있는 권한이 있어야 합니다. 할당 받은 권한 수준에 따라 보고 관리할 수 있는 항목이 결정됩니다. 자세한 내용은 [Management Studio에서 보고서 서버에 연결](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)합니다.  
  
 **인증**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 제공한 사용자 지정 인증 확장 프로그램이 처리하는 Windows 인증 요청 또는 폼 인증 요청을 받아들이도록 구성할 수 있습니다. Reporting Services에 연결할 때는 다음 인증 모드 중 하나를 선택합니다.  
  
 **Windows 인증 모드(Windows 인증)**  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 자격 증명을 사용하여 보고서 서버 인스턴스에 연결합니다.  
  
 **기본 인증**  
 Reporting Services 설치에서 기본 인증을 사용하도록 구성되어 있는 경우 **기본 인증** 을 사용하여 연결합니다.  
  
 **폼 인증**  
 Reporting Services 설치에서 사용자 지정 인증 확장 프로그램을 사용하도록 구성되어 있는 경우 **폼 인증** 을 사용하여 연결합니다.  
  
 **사용자 이름**  
 연결에 사용할 로그인 이름을 입력합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 선택한 경우에만 사용할 수 있습니다.  
  
 **암호**  
 사용자 이름에 대한 암호를 입력합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 선택한 경우에만 편집할 수 있습니다.  
  
 **암호 저장**  
 입력한 암호를 저장합니다. 이 옵션은 **옵션**을 클릭한 경우에만 표시되며 **기본 인증** 또는 **폼 인증**을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다.  
  
 **연결**  
 선택한 서버에 연결합니다.  
  
 **옵션**  
 암호 저장과 같은 추가 서버 연결 옵션을 표시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 데이터베이스 연결 구성 &#40;SSRS 구성 관리자&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Management Studio에서 보고서 서버에 연결](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [보고서 서버 인증](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
