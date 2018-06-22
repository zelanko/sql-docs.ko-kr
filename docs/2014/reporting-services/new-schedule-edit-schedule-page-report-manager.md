---
title: '새 일정: 일정 편집 페이지 (보고서 관리자) | Microsoft Docs'
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 52a4d250-e185-4116-a29c-d809940a00fb
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 019cb1a12e25ac3c347d1dbdb72296c2f2a888f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089901"
---
# <a name="new-schedule-edit-schedule-page-report-manager"></a>새 일정: 일정 편집 페이지 (보고서 관리자)
  새 일정/일정 편집 페이지를 사용하여 보고서에 대한 일정을 만들 수 있습니다. 일정은 캐시된 보고서를 새로 고치고 보고서 기록에 또는 독립 실행 항목으로 스냅숏을 만들기 위해 구독에서 사용됩니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 참조 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 무인 모드로 실행될 수 있는 보고서에 대해서만 일정을 만들 수 있습니다. 보고서를 무인 모드로 실행하려면 보고서 서버 데이터베이스에 보고서 데이터 원본 자격 증명을 저장해야 합니다. 자세한 내용은 참조 [데이터 원본 속성 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md)합니다.  
  
 일부 빈도 조합은 단일 일정으로 지원되지 않습니다. 예를 들어 매주 금요일 오후 12시와 4시에 보고서를 실행하려면 실행 날짜가 금요일, 시작 시간이 오후 12시와 4시로 지정된 두 개의 일별 일정을 만들어야 합니다.  
  
 일정 처리는 일정을 호스팅하고 처리하는 보고서 서버의 현지 시간을 기준으로 합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-execution-properties-page-of-a-report"></a>보고서의 실행 속성 페이지에서 새 일정 또는 일정 편집 페이지를 열려면  
  
1.  보고서 관리자를 열고 일정을 구성할 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 모델의 일반 속성 페이지가 열립니다.  
  
4.  **실행** 탭을 선택합니다.  
  
5.  **보고서 실행 스냅숏에서 이 보고서 렌더링**옵션을 선택합니다. 그런 다음 **다음 일정을 사용하여 스냅숏을 보고서 기록에 추가**, **보고서별 일정**을 차례로 선택한 후 **구성**을 클릭합니다.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-history-properties-page-of-a-report"></a>보고서의 기록 속성 페이지에서 새 일정 또는 일정 편집 페이지를 열려면  
  
1.  보고서 관리자를 열고 일정을 구성할 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 모델의 일반 속성 페이지가 열립니다.  
  
4.  **기록** 탭을 선택합니다.  
  
5.  **다음 일정을 사용하여 스냅숏을 보고서 기록에 추가**, **보고서별 일정**을 차례로 선택한 후 **구성**을 클릭합니다.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-subscriptions-page"></a>구독 페이지에서 새 일정 또는 일정 편집 페이지를 열려면  
  
1.  보고서 관리자를 열고 일정을 구성할 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 다음을 수행합니다.  
  
    -   **관리**를 클릭합니다. 보고서의 일반 속성 페이지가 열립니다. **구독** 탭을 선택합니다.  
  
    -   **구독**을 클릭합니다. 보고서의 **구독** 속성 페이지가 열립니다.  
  
4.  도구 모음에서 **새 구독** 을 클릭하거나 편집할 기존 구독을 선택합니다.  
  
5.  **구독 처리 옵션**에서 **새 일정**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **일정 세부 정보**  
 보고서 실행 시간과 빈도를 지정하는 옵션을 선택합니다. 빈도 옵션은 계층적입니다. 첫째 옵션 집합은 빈도 범주(시간별, 일별, 주별 등)를 지정합니다. 둘째 옵션 집합은 처음 선택에 따라 표시됩니다.  
  
-   **시간** 은 시간 간격으로 실행되는 일정을 정의합니다. 일정을 실행할 날짜를 지정하려면 **시작 및 끝 날짜** 섹션을 사용합니다.  
  
-   **일** 은 선택하는 요일의 특정 시간 및 분에 실행되는 일정을 정의합니다. 다음과 같은 방법으로 일을 지정할 수 있습니다: 모든 \< *일*>, 주중 매일, 매 \< *번호*> 일 합니다. 한 가지 방법을 선택하면 다른 날이 선택된 것처럼 보이더라도 다른 방법은 사용할 수 없게 됩니다.  
  
-   **주** 는 주별 간격으로 특정 시간 및 분에 실행되는 일정을 정의합니다. 간격은 주 전체(예: 격주간)나 주 중의 요일로 지정할 수 있습니다.  
  
-   **월** 은 월별로 실행되는 일정을 정의합니다. 월에서 패턴에 따른 날짜(예: 매월 마지막 일요일)나 특정 달력 날짜(예: 매월 1일과 15일을 나타내는 1과 15)를 선택할 수 있습니다. 쉼표와 하이픈을 사용하여 여러 날짜와 범위를 지정할 수 있습니다(예: 1, 5, 7-12, 21).  
  
-   **한 번** 은 한 번만 실행되는 일정을 정의합니다. 일정을 실행할 날짜를 지정하려면 **시작 및 끝 날짜** 섹션을 사용합니다. 이 일정은 처리되는 즉시 만료됩니다.  
  
 **시작 및 종료 날짜**  
 일정이 개시되는 시작 날짜와 일정이 만료되는 끝 날짜를 지정합니다.  
  
 일정은 별도의 알림 메시지 없이 만료됩니다. 끝 날짜 이후에는 일정이 더 이상 실행되지 않습니다. 만료된 일정은 삭제되지 않습니다. 일정은 수동으로 삭제해야 합니다. 따라서 일정이 계속되도록 선택하면 끝 날짜를 연장할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [일정 만들기, 수정 및 삭제](subscriptions/create-modify-and-delete-schedules.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  