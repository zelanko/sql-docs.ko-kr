---
title: "스냅샷 사용(웹 포털) | Microsoft Docs"
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ae20556-e243-4a60-b076-9fd9e82c7355
caps.latest.revision: "6"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7498112d3822d18976ea6482c6014ce7bc69435f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="working-with-snapshots-web-portal"></a>스냅숏 사용(웹 포털)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

보고서에 대한 스냅숏을 만든 경우 보고서의 **줄임표(...)** , **관리** 를 선택하고 **캐싱** 또는 **기록 스냅숏**을 선택하여 제어할 수 있습니다.  
  
> [!NOTE]
> SQL Server 에이전트 서비스를 시작해야 합니다.  
   
캐시 스냅숏을 만들어 특정 실행 속성의 더 빠른 로드를 허용할 수 있습니다. 기록 스냅숏을 사용하여 특정 시점을 캡처할 수도 있습니다.  
  
## <a name="creating-a-cache-snapshot"></a>캐시 스냅숏 만들기  
  
다음을 수행하여 스냅숏을 만들 수 있습니다.  
  
![ssRSWebPortal-report-caching4](../reporting-services/media/ssrswebportal-report-caching4.png)  
  
1.  **캐싱** 페이지에서 **항상 사전 생성된 스냅숏에 대해 이 보고서 실행** 을 선택하여 스냅숏을 만들기 위한 옵션을 사용할 수 있습니다.  
  
2.  되풀이 스냅숏을 예약하려면 **일정에 따라 캐시 스냅숏 만들기** 를 선택합니다. 그런 다음 공유 일정을 사용하거나 사용자 지정 일정을 정의하여 스냅숏을 새로 고칠 수 있습니다.  
  
3.  지금 바로 캐시 스냅숏을 만들려면 **이 페이지에서 적용을 클릭할 때 캐시 스냅숏 만들기** 를 선택합니다. 이 옵션만 선택하는 경우 스냅숏은 새로 고쳐지지 않습니다.  
  
## <a name="create-modify-and-delete-history-snapshots"></a>기록 스냅숏 만들기, 수정 및 삭제  
  
기록 스냅숏으로 작업하려면 보고서를 관리하고 **기록 스냅숏**을 선택합니다.  
  
**기록 스냅숏** 페이지를 사용하여 시간에 따라 생성 및 저장된 보고서 스냅숏을 볼 수 있습니다. 보고서 서버에 설정된 옵션에 따라 기록에 최근 스냅숏만 포함되어 있을 수 있습니다.  
  
보고서 기록은 항상 이 기록의 원본으로 사용되는 보고서의 컨텍스트 내에서 볼 수 있습니다. 보고서 서버의 모든 보고서 기록을 한 곳에서 볼 수는 없습니다.  
  
기록 스냅숏을 생성하려면 보고서가 무인 모드로 실행될 수 있어야 합니다. 즉, 보고서에서 저장된 자격 증명을 사용해야 하며, 매개 변수 있는 보고서의 경우 모든 매개 변수에 대한 기본 매개 변수 값을 포함해야 합니다. 보고서 기록은 수동으로 또는 예약된 작업으로 생성할 수 있습니다. 보고서의 기록 속성에 따라 보고서 기록을 만드는 방법이 지정됩니다.  
  
![ssRSWebPortal-historysnapshots1](../reporting-services/media/ssrswebportal-historysnapshots1.png)  
   
1.  기록 스냅숏을 만들려면 **+ 새 기록 스냅숏**을 선택합니다. 여기서 보고서를 처리하고 목록에 항목을 추가합니다.  
  
2.  일정 및 보존 정책을 정의하는 설정으로 이동할 수 있습니다.  
  
3.  기록 스냅숏을 선택하면 이를 볼 수 있습니다. 보고서 기록에 표시되는 스냅숏은 스냅숏이 만들어진 날짜와 시간으로만 구별됩니다. 스냅숏이 예약된 작업에 따라 생성된 것인지 수동 작업으로 생성된 것인지는 시각적으로 구분할 수 없습니다.  
  
### <a name="schedule-and-settings"></a>일정 및 설정  
  
**일정 및 설정** 을 선택하면 일정에 추가 옵션을 제공하고 생성된 스냅숏의 보존 일정을 제어합니다.  
  
![ssRSWebPortal-historysnapshots2](../reporting-services/media/ssrswebportal-historysnapshots2.png)  
   
필요에 따라 스냅숏 생성에 대한 일정을 만들 수 있습니다. 또한 다른 사용자가 새 스냅숏을 만드는 것을 방지할 수 있습니다. **사람들이 스냅숏을 수동으로 만들 수 있도록 허용** 을 선택 취소하면 **+ 새 스냅숏 기록 단추**를 사용할 수 없게 됩니다.  
  
원하는 스냅숏 보존 방법을 정의할 수도 있습니다.  
  
**보고서 기록에 캐시 스냅숏도 저장**  
  
보고서 실행 속성에 따라 생성하는 보고서 스냅숏을 보고서 기록에 복사하려면 이를 선택합니다. 생성된 스냅숏에서 보고서를 실행하도록 보고서 실행 속성을 설정할 수 있습니다. 이 보고서 기록 속성을 설정하면 스냅숏의 복사본을 보고서 기록에 저장하여 시간에 따라 생성되는 모든 보고서 스냅숏에 대한 기록을 보관할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[웹 포털](../reporting-services/web-portal-ssrs-native-mode.md)  
[페이지를 매긴 보고서 사용](working-with-paginated-reports-web-portal.md)  
[공유 데이터 집합 작업](../reporting-services/work-with-shared-datasets-web-portal.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
