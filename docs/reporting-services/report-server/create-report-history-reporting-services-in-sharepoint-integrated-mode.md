---
title: 보고서 기록 만들기(SharePoint 통합 모드의 Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report history [Reporting Services], SharePoint
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4003f100ea918a6b197d1806aeec18279955cc45
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="create-report-history-reporting-services-in-sharepoint-integrated-mode"></a>보고서 기록 만들기(SharePoint 통합 모드의 Reporting Services)
  보고서 기록은 시간에 따라 만든 보고서 스냅숏의 모음입니다. 각 스냅숏은 생성 당시의 상태를 그대로 나타내는 보고서 복사본입니다. 스냅숏 생성 당시의 보고서 레이아웃 및 데이터가 포함됩니다. 렌더링 정보는 스냅숏에 저장되지 않습니다. 보고서 기록의 스냅숏을 열면 보고서 뷰어 웹 파트에 HTML로 열립니다. 렌더링된 후 스냅숏을 다른 응용 프로그램 형식으로 내보낼 수 있습니다.  
  
 보고서 기록을 만들려면 보고서가 무인 모드로 실행될 수 있어야 합니다. 즉, 보고서 서버가 사용자와 상호 작용하지 않고 보고서를 실행할 수 있어야 합니다. 해당 보고서가 포함된 라이브러리에 대한 항목 편집 권한이 있어야 합니다. 보고서 기록을 보거나 삭제하려면 버전 보기 또는 버전 삭제 권한이 있어야 합니다.  
  
### <a name="to-create-a-snapshot-or-report-history-on-demand"></a>요청 시 스냅숏 또는 보고서 기록을 만들려면  
  
1.  보고서를 가리킵니다.  
  
2.  클릭하여 아래쪽 화살표를 표시한 다음 **보고서 기록 보기**를 선택합니다.  
  
3.  **새 스냅숏**을 클릭합니다. 단추가 표시되지 않는 경우 보고서 기록에 스냅숏을 만들 수 있는 권한이 없기 때문입니다.  
  
4.  방금 만든 스냅숏을 보려면 목록에서 선택합니다. 각 스냅숏은 스냅숏이 생성된 시기를 보여 주는 타임스탬프로 식별됩니다. 스냅숏의 이름을 바꾸거나, 다른 위치로 이동하거나, 수정할 수는 없습니다.  
  
### <a name="to-schedule-report-history"></a>보고서 기록을 예약하려면  
  
1.  보고서를 가리킵니다.  
  
2.  클릭하여 아래쪽 화살표를 표시한 다음 **처리 옵션 관리**를 선택합니다.  
  
3.  **기록 스냅숏 옵션**에서 **일정에 따라 보고서 기록 스냅숏 만들기**를 클릭합니다.  
  
4.  사용할 일정 정보가 포함된 공유 일정이 있는 경우 **공유 일정** 을 클릭하고 사용할 일정을 선택합니다. 또는 **사용자 지정 일정**, **구성** 을 차례로 클릭하여 되풀이 일정으로 보고서 기록을 만드는 옵션을 지정합니다.  
  
### <a name="to-create-report-history-when-data-is-refreshed-in-a-report"></a>보고서에서 데이터를 새로 고칠 때 보고서 기록을 만들려면  
  
1.  보고서를 가리킵니다.  
  
2.  클릭하여 아래쪽 화살표를 표시한 다음 **처리 옵션 관리**를 선택합니다.  
  
3.  **기록 스냅숏 옵션**에서 **보고서 기록에 모든 보고서 데이터 스냅숏 저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  
