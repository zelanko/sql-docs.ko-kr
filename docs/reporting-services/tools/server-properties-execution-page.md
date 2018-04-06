---
title: 서버 속성(실행 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.execution.f1
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8fae6a61597c42a73a354ed84fb8b0287f448194
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="server-properties-execution-page"></a>서버 속성(실행 페이지)
  이 페이지를 사용하여 보고서 실행 제한 시간 값을 설정할 수 있습니다. 이 값은 현재 보고서 서버 인스턴스에서 처리하는 모든 보고서에 적용됩니다. 개별 보고서에 대해 이 값을 다시 정의할 수 있습니다. 보고서 서버에서 수행되는 모든 보고서 처리와 보고서 서버가 보고서에 사용되는 데이터를 검색할 때 데이터베이스에서 수행되는 쿼리 처리를 감안하여 값을 지정해야 합니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작하고 보고서 서버 인스턴스에 연결한 다음 보고서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **실행** 을 클릭하여 이 페이지를 엽니다.  
  
## <a name="options"></a>변수  
 **보고서 실행 시간을 제한 안 함**  
 보고서 서버에서 보고서 처리를 완료하는 시간을 제한하지 않습니다.  
  
 **보고서 실행 시간을 다음으로 제한(초)**  
 보고서 실행에 대한 시간 제약을 설정합니다. 시간은 보고서 요청 시점부터 계산됩니다. 보고서가 완전히 처리되기 전에 제한 시간에 도달하면 보고서 서버에서는 해당 프로세스 및 외부 데이터 원본에 대한 in-process 쿼리를 취소합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)   
 [보고서 및 공유 데이터 집합 처리에 대한 제한 시간 값 설정&#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
