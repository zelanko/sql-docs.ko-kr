---
title: 서버 속성(로깅 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a04c27fd790a1ad5c4ba453b43af5983a6440e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099524"
---
# <a name="server-properties-logging-page"></a>서버 속성(로깅 페이지)
  이 페이지를 사용하여 보고서 서버에서 수집한 보고서 실행 데이터에 대한 제한을 설정할 수 있습니다. 실행 데이터는 보고서 서버 데이터베이스에 내부적으로 저장됩니다. 기본 모드 또는 SharePoint 통합 모드로 실행되는 보고서 서버에 대한 보고서 작업을 추적할 수 있습니다. 보고서 서버가 스케일 아웃 배포에 포함되는 경우 보고서 실행 로그는 단일 로그 파일에 전체 배포에 대한 모든 보고서 작업 기록을 유지합니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 열고 보고서 서버에 연결한 다음 보고서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **로깅** 을 클릭하여 이 페이지를 엽니다.  
  
## <a name="options"></a>변수  
 **보고서 실행 로깅 사용**  
 서버의 보고서 작업에 대한 정보를 작성하고 저장하려면 클릭합니다. 이 옵션을 설정하면 보고서 서버는 사용된 보고서, 보고서 처리 빈도, 수행된 보고서 작업의 유형, 출력 형식 및 보고서를 실행한 사용자를 추적합니다. 로그에 캡처되는 추가 데이터 지점에 대 한 자세한 내용은 참조 하세요. [보고서 서버 실행 로그 및 ExecutionLog3 뷰](../report-server/report-server-executionlog-and-the-executionlog3-view.md)합니다.  
  
 **다음 일 수보다 오래된 로그 항목 제거**  
 보고서 실행 로그에서 로그 항목을 지우기 전에 경과해야 하는 일 수를 지정합니다. 기본값은 60일입니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 로그 파일 및 소스](../report-server/reporting-services-log-files-and-sources.md)   
 [Management Studio의 보고서 서버 F1 도움말](report-server-in-management-studio-f1-help.md)   
 [보고서 서버 실행 로그 및 ExecutionLog3 뷰](../report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
