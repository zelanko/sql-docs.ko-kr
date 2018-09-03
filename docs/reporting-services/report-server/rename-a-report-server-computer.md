---
title: 보고서 서버 컴퓨터 이름 바꾸기 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- renaming report servers
ms.assetid: 82fc4ba2-291a-4939-a025-271b8d687c54
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bfa856c392dd133ff94c4079faceea95f5c422b0
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43270605"
---
# <a name="rename-a-report-server-computer"></a>보고서 서버 컴퓨터 이름 바꾸기
  컴퓨터 이름을 바꾸면 웹 서버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 같은 컴퓨터에 있는 경우 이에 해당하는 이름이 변경됩니다. 컴퓨터 이름을 변경한 다음에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 액세스할 수 없는 경우도 있습니다. 컴퓨터 이름을 변경한 다음에는 이 항목의 단계를 사용하여 보고서 서버를 다시 구성합니다.  
  
## <a name="renaming-a-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진 이름 바꾸기  
 보고서 서버 데이터베이스를 실행하는  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 이름을 바꾸는 경우 다음을 수행하십시오.  
  
1.  Reporting Services 구성 도구를 시작한 다음 이름이 바뀐 서버에 있는 보고서 서버 데이터베이스를 사용하는 보고서 서버에 연결합니다.  
  
2.  데이터베이스 설치 페이지를 엽니다.  
  
3.  **서버 이름**에서 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이름을 입력하거나 선택한 다음 **연결**을 클릭합니다.  
  
4.  **적용**을 클릭합니다.  
  
 보고서 서버에서 로컬 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 사용하는 경우 *(local)* 또는 *(local)\instancename* 을 사용하여 서버를 지정할 수 있습니다. *(local)* 을 사용하여 서버를 참조하는 경우에는 서버 이름을 바꿔도 연결에 문제가 생기지 않습니다. 원격 서버를 사용하거나 서버 이름을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 구성하는 경우에는 서버 이름을 변경할 때마다 데이터베이스 연결 정보를 업데이트해야 합니다.  
  
## <a name="renaming-a-report-server-computer"></a>보고서 서버 컴퓨터 이름 바꾸기  
 보고서 서버를 실행하는 컴퓨터의 이름을 바꾸는 경우 다음을 수행하십시오.  
  
1.  텍스트 편집기에서 RSReportServer.config를 연 다음 **UrlRoot** 설정을 수정하여 새 서버 이름을 반영합니다. **UrlRoot** 설정은 배달 확장 프로그램에서 보고서 서버에 저장된 항목 액세스에 사용하는 URL을 작성하는 데 사용됩니다. 보고서 서버 URL 주소를 변경하려면 구독이 계속 보고서를 배달하도록 **UrlRoot** 설정을 업데이트해야 합니다.  
  
2.  동일한 파일에서 설정하는 경우 **ReportServerUrl** 설정을 수정하여 새 서버 이름을 반영합니다. 이 설정이 모든 설치에 사용되는 것은 아닙니다. 이 설정이 비어 있는 경우 아무 작업도 수행하지 마십시오.  
  
    > [!NOTE]  
    >  회사 네트워크에서 WINS(Windows Internet Naming Service)를 사용하는 경우 보고서 서버와 보고서 관리자가 일정 기간 동안 이전 이름으로 사용 가능하다고 표시될 수 있습니다. WINS에서는 서비스하는 각 컴퓨터에 IP 주소를 매핑합니다. WINS에서 이름이 바뀐 컴퓨터의 IP 주소를 새로 고친 다음에는 더 이상 이전 컴퓨터 이름을 사용하여 보고서 서버나 보고서 관리자에 액세스할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [RSReportServer 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [보고서 서버 서비스 시작 및 중지](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [rsconfig 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)  
  
  
