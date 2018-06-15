---
title: 서버 속성(로깅 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 46142ee40d08b217effd89717b675c36a555904b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33029670"
---
# <a name="server-properties-logging-page"></a>서버 속성(로깅 페이지)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 의 이 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 페이지를 사용하여 보고서 서버에서 수집한 보고서 실행 데이터에 대한 제한을 설정할 수 있습니다. 실행 데이터는 보고서 서버 데이터베이스에 내부적으로 저장됩니다. 기본 모드 또는 SharePoint 통합 모드로 실행되는 보고서 서버에 대한 보고서 작업을 추적할 수 있습니다. 보고서 서버가 스케일 아웃 배포에 포함되는 경우 보고서 실행 로그는 단일 로그 파일에 전체 배포에 대한 모든 보고서 작업 기록을 유지합니다.  
  
 이 페이지를 열려면
 1) 시작 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) 보고서 서버에 연결합니다.
 3) 보고서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다. 
 4) **로깅** 을 클릭하여 이 페이지를 엽니다.  
  
## <a name="options"></a>변수  
 **보고서 실행 로깅 사용**  
 서버의 보고서 작업에 대한 정보를 작성하고 저장하려면 클릭합니다. 이 옵션을 설정하면 보고서 서버는 사용된 보고서, 보고서 처리 빈도, 수행된 보고서 작업의 유형, 출력 형식 및 보고서를 실행한 사용자를 추적합니다. 로그에 캡처되는 추가 데이터 지점에 대한 자세한 내용은 [보고서 서버 ExecutionLog 및 ExecutionLog3 뷰](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)를 참조하세요.  
  
 **다음 일 수보다 오래된 로그 항목 제거**  
 보고서 실행 로그에서 로그 항목을 지우기 전에 경과해야 하는 일 수를 지정합니다. 기본값은 60일입니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 로그 파일 및 소스](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [보고서 서버 ExecutionLog 및 ExecutionLog3 뷰](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
