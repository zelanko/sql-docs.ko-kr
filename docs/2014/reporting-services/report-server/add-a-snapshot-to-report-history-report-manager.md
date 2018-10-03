---
title: 보고서 기록에 스냅숏 추가(보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report history [Reporting Services], adding snapshots
- historical data [Reporting Services]
- snapshots [Reporting Services], adding report snapshots
- adding snapshots to report history
- report snapshots [Reporting Services], adding
ms.assetid: 3aafb183-789e-46ac-966c-881dc549b31d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e0c9e553ebff35c865adabfeea164a56b5cffce0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075973"
---
# <a name="add-a-snapshot-to-report-history-report-manager"></a>보고서 기록에 스냅숏 추가(보고서 관리자)
  보고서 기록은 시간에 따라 만든 보고서 스냅숏의 모음입니다. 보고서 스냅숏은 레이아웃 정보 및 특정 시점에 검색된 쿼리 결과가 들어 있는 보고서입니다. 보고서를 선택할 때 최신 쿼리 결과를 얻을 수 있는 요청 시 실행 보고서와 달리 보고서 스냅숏은 예약된 시간에 처리되고 보고서 서버에 저장됩니다. 표시할 보고서 스냅숏을 선택하면 보고서 서버가 보고서 서버 데이터베이스에서 저장된 보고서를 검색하고 스냅숏이 만들어진 시점에 따른 보고서의 현재 데이터 및 레이아웃을 표시합니다.  
  
 보고서 스냅숏은 특정 렌더링 형식으로 저장되지 않으며 사용자나 응용 프로그램이 보고서 스냅숏을 요청할 때만 HTML과 같은 최종 보기 형식으로 렌더링됩니다. 지연된 렌더링은 스냅숏을 이동 가능하게 만듭니다. 요청 장치나 웹 브라우저에 적합한 형식으로 보고서를 렌더링할 수 있습니다.  
  
### <a name="to-manually-add-snapshots-to-report-history"></a>보고서 기록에 스냅숏을 수동으로 추가하려면  
  
1.  보고서 관리자에서 **내용** 페이지로 이동하고 기록을 보려는 항목을 마우스로 가리킨 다음 드롭다운 화살표를 클릭합니다.  
  
2.  드롭다운 메뉴에서 **보고서 기록 보기**를 클릭합니다.  
  
3.  **새 스냅숏**을 클릭합니다. **실행 날짜** 열에 새 스냅숏이 생성됩니다.  
  
    > [!NOTE]  
    >  이를 위해 관리자는 보고서 기록을 **수동으로 기록 작성 허용**상태로 구성해야 합니다. 자세한 내용은 [보고서 기록 제한 &#40;보고서 관리자&#41;](../reports/limit-report-history-report-manager.md)합니다.  
  
4.  **적용**을 클릭합니다.  
  
### <a name="to-automatically-add-all-snapshots-to-report-history"></a>보고서 기록에 모든 스냅숏을 자동으로 추가하려면  
  
1.  보고서 실행 스냅숏으로 실행하도록 구성된 보고서의 경우 스냅숏이 새로 고쳐질 때마다 보고서 기록에 스냅숏 복사본을 저장하도록 추가 속성을 설정할 수 있습니다.  
  
2.  보고서 관리자에서 **내용** 페이지로 이동하고 기록을 보려는 항목을 마우스로 가리킨 다음 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다.  
  
4.  **스냅숏 옵션**을 클릭합니다.  
  
5.  **모든 보고서 실행 스냅숏을 기록에 저장**확인란을 선택합니다.  
  
6.  **적용**을 클릭합니다.  
  
### <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>일정에 따라 보고서 기록에 스냅숏을 자동으로 추가하려면  
  
1.  보고서 관리자에서 **내용** 페이지로 이동하고 기록을 보려는 항목을 마우스로 가리킨 다음 드롭다운 화살표를 클릭합니다.  
  
2.  드롭다운 메뉴에서 **관리**를 클릭합니다.  
  
3.  **스냅숏 옵션**을 클릭합니다.  
  
4.  **다음 일정을 사용하여 스냅숏을 보고서 기록에 추가**확인란을 선택합니다. 다음 중 하나를 수행합니다.  
  
    -   **보고서별 일정**을 선택합니다. 일정 정보를 채우고 일정의 시작일과 종료일을 선택한 후 **확인**을 클릭합니다.  
  
    -   **공유 일정**을 선택합니다. 목록에서 원하는 일정을 선택합니다.  
  
5.  **적용**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 실행 속성 구성 &#40;보고서 관리자&#41;](../reports/configure-execution-properties-for-a-report-report-manager.md)   
 [열기 및 닫기 보고서 &#40;보고서 관리자&#41;](../reports/open-and-close-a-report-report-manager.md)   
 [보고서 기록 제한&#40;보고서 관리자&#41;](../reports/limit-report-history-report-manager.md)   
 [일정](../subscriptions/schedules.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)  
  
  
