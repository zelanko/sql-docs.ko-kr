---
title: 서버 속성(일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 905d673939c1831cbe84d49e863ec401a03ec4b6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290269"
---
# <a name="server-properties-general-page"></a>서버 속성(일반 페이지)
  이 페이지를 사용하여 보고서 관리자에 사용된 제목을 보거나 수정하고, 내 보고서를 설정 또는 해제하고, 내 보고서의 보안에 대한 역할 정의를 선택하고 클라이언트 인쇄 컨트롤을 설정 또는 해제할 수 있습니다.  
  
 이 페이지를 열려면 시작 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 보고서 서버 인스턴스에 연결할 보고서 서버 이름을 마우스 오른쪽 단추로 클릭 및 선택한 **속성**합니다.  
  
 서버 모드에 따라 설정할 수 있는 서버 속성이 결정됩니다. SharePoint 통합 모드로 구성된 보고서 서버를 관리하는 경우 내 보고서를 활성화하거나 보고서 관리자에 대한 응용 프로그램 제목을 설정할 수 없습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 보고서 관리자에 표시될 응용 프로그램 이름을 입력합니다. 기본적으로 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]입니다. 지정한 이름은 보고서 관리자에만 나타납니다.  
  
 **버전(Version)**  
 이 속성은 읽기 전용입니다. 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 버전을 지정합니다.  
  
 **버전(Edition)**  
 이 속성은 읽기 전용입니다. 현재 보고서 서버 인스턴스를 지정합니다. 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 보고서 관리자를 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 **인증 모드**  
 이 속성은 읽기 전용입니다. 보고서 서버 인스턴스에서 허용되는 인증 요청의 유형을 식별합니다. 인증 모드를 변경하려면 RSReportServer.config 파일을 편집해야 합니다. 자세한 내용은 [Authentication with the Report Server](../security/authentication-with-the-report-server.md)을(를) 참조하세요.  
  
 **URL**  
 이 속성은 읽기 전용입니다. 보고서 서버 웹 서비스에 대한 URL을 지정합니다. 이 값은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에 지정됩니다. 자세한 내용은 [URL 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)을 참조하세요.  
  
 **각 사용자에 대해 내 보고서 폴더 설정**  
 사용자가 내 보고서를 사용할 수 있도록 합니다. 이 옵션은 기본 모드 보고서 서버에서만 사용할 수 있습니다.  
  
 **각 내 보고서 폴더에 적용할 역할을 선택하십시오.**  
 내 보고서의 보안에 사용할 역할 정의를 지정합니다. 역할 정의는 각 내 보고서 폴더에서 지원되는 태스크 집합을 식별합니다.  
  
 **ActiveX 클라이언트 인쇄 컨트롤에 대 한 다운로드 설정**  
 집합의 `EnableClientPrinting` 보고서 서버 시스템 속성이 있습니다. 클라이언트 인쇄를 설정하는 경우 로컬 관리자 권한을 가진 사용자는 HTML 보고서 인쇄를 위한 서명된 ActiveX 컨트롤을 다운로드할 수 있습니다. 자세한 내용은 [설정 및 Reporting Services에 대 한 클라이언트 쪽 인쇄 사용 안 함](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](connect-to-a-report-server-in-management-studio.md)   
 [내 보고서 사용 및 사용 안 함 설정](../report-server/enable-and-disable-my-reports.md)   
 [Management Studio의 보고서 서버 F1 도움말](report-server-in-management-studio-f1-help.md)   
 [내 보고서 보안](../security/secure-my-reports.md)  
  
  
