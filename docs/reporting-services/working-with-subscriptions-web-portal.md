---
title: "구독 사용(웹 포털) | Microsoft Docs"
ms.custom: 
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09e8ece5-0200-41f2-87c1-9fab19e261be
caps.latest.revision: "6"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 770147e3bed0f660127938ba1b2f0ae955954e62
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="working-with-subscriptions-web-portal"></a>구독 작업(웹 포털)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

구독 페이지를 사용하여 현재 보고서의 구독을 모두 나열할 수 있습니다. 모든 구독 태스크 관리가 뜻하는 바와 같이 충분한 권한이 있으면 모든 사용자의 구독을 볼 수 있습니다. 그렇지 않으면 이 페이지는 사용자가 소유하는 구독만 표시합니다.  
  
새 구독을 만들기 전에 보고서 데이터 원본에서 저장된 자격 증명을 사용하는지 확인해야 합니다. 자격 증명을 저장하려면 데이터 원본 속성 페이지를 사용하십시오.  
  
> [!NOTE]
> SQL Server 에이전트 서비스를 시작해야 합니다.   
  
![ssRSWebPortal-subscriptions1](../reporting-services/media/ssrswebportal-subscriptions1.png)  
   
보고서의 **줄임표(...)** , **관리** , **구독**을 차례로 선택하면 구독 페이지에 액세스할 수 있습니다.  
  
구독 페이지에서 **+ 새 구독**을 선택하면 새 구독을 만들 수 있습니다. 기존 구독을 편집하거나 선택한 구독을 삭제할 수도 있습니다.  
  
이 페이지의 **결과** 열에는 구독 실행의 결과 상태도 제공됩니다. 구독에 대한 오류가 발생한 경우 먼저 결과 열을 검사하여 메시지 내용을 확인하는 것이 좋습니다.  
  
## <a name="creating-or-editing-a-subscription"></a>구독 만들기 또는 편집  
새 구독 또는 구독 편집 페이지를 사용하여 보고서에 대한 새 구독을 만들거나 기존 구독을 수정할 수 있습니다. 이 페이지의 옵션은 사용자의 역할 할당에 따라 다릅니다. 고급 권한이 있는 사용자는 추가 옵션으로 작업할 수 있습니다.  
  
구독은 무인 모드로 실행될 수 있는 보고서에 대해 지원됩니다. 이 보고서는 저장된 자격 증명을 사용하거나 자격 증명을 사용하지 않아야 합니다. 보고서에서 매개 변수를 사용하는 경우에는 기본값을 지정해야 합니다. 보고서 실행 설정을 변경하거나 매개 변수 속성에서 사용하는 기본값을 제거하면 구독이 비활성 상태로 바뀔 수 있습니다. 자세한 내용은 [기본 모드 보고서 서버에 대한 구독 만들기 및 관리]를 참조하세요.  
  
### <a name="type-of-subscription"></a>구독 유형  
**표준 구독** 및 **데이터 기반 구독**할 수 있습니다.  
  
![ssRSWebPortal-subscriptions3](../reporting-services/media/ssrswebportal-subscriptions3.png)  
   
데이터 기반 구독은 구독이 실행될 때마다 구독자 데이터베이스에 구독 정보를 쿼리하는 구독입니다. 데이터 기반 구독은 쿼리 결과를 사용하여 구독을 받는 사람, 배달 설정 및 보고서 매개 변수 값을 확인합니다. 실행할 때 보고서 서버는 쿼리를 실행하여 구독 설정에 사용된 값을 가져옵니다.   
  
데이터 기반 구독을 만들려면 구독 데이터를 가져오는 쿼리 또는 명령의 작성 방법을 알아야 합니다. 또한 구독에 사용할 구독자 데이터(예: 구독자 이름 및 전자 메일 주소)를 포함하는 데이터 저장소가 있어야 합니다.  
  
이 옵션은 고급 권한이 있는 사용자가 사용할 수 있습니다. 기본 보안을 사용할 경우 내 보고서 폴더에 있는 보고서에 대해서는 데이터 기반 구독을 사용할 수 없습니다.  
  
### <a name="destination"></a>대상  
보고서를 배포하는 데 사용할 배달 확장 프로그램을 선택합니다.   
  
배달 확장 프로그램의 가용성은 보고서 서버에 설치 및 구성되었는지 여부에 따라 다릅니다. 보고서 서버 전자 메일은 기본 배달 확장 프로그램이지만 먼저 구성을 해야 사용할 수 있습니다. 파일 공유 배달은 구성이 필요하지 않지만 먼저 공유 폴더를 정의해야 사용할 수 있습니다.  
  
![ssRSWebPortal-subscriptions2](../reporting-services/media/ssrswebportal-subscriptions2.png)  
  
선택한 배달 확장 프로그램에 따라 다음 설정이 표시됩니다.  
  
-   메일 구독은 메일 사용자에게 익숙한 필드(예: 받는 사람, 제목 및 우선 순위 필드)를 제공합니다. 보고서를 포함시키거나 첨부하려면 **보고서 포함** 을 지정하고 보고서에 대한 URL을 포함시키려면 **링크 포함** 을 지정합니다. 첨부 또는 포함된 보고서의 표시 형식을 선택하려면 **렌더링 형식** 을 지정합니다.  
  
-   파일 공유 구독은 대상 위치를 지정할 수 있도록 허용하는 필드를 제공합니다. 모든 보고서를 파일 공유로 배달할 수 있습니다. 그러나 대화형 기능을 지원하는 보고서(관련 행 및 열에 대한 드릴다운을 지원하는 행렬 보고서 포함)는 정적 파일로 렌더링됩니다. 드릴다운 행 및 열은 정적 파일에서 볼 수 없습니다. 파일 공유 이름은 UNC(Uniform Naming Convention) 형식(예: \mycomputer\public\myreportfiles)으로 지정해야 합니다. 경로 이름 뒤에 백슬래시를 사용하지 마십시오. 보고서 파일은 렌더링 형식을 기반으로 하는 파일 형식으로 배달됩니다. 예를 들어 Excel을 선택할 경우 보고서는 .xlsx 파일로 배달됩니다.  
  
### <a name="data-driven-subscription-dataset"></a>데이터 기반 구독 데이터 집합  
데이터 기반 구독의 경우 구독에 사용되는 데이터 집합을 정의해야 합니다. **데이터 집합 편집** 을 선택하여 해당 정보를 제공합니다.  
  
![ssRSWebPortal-subscriptions4](../reporting-services/media/ssrswebportal-subscriptions4.png)  
  
먼저 쿼리에 사용할 **데이터 원본** 을 지정해야 합니다. 공유 데이터 원본이거나 사용자 지정 데이터 원본을 지정할 수 있습니다.  
  
구독을 실행하는 데 필요한 다양한 옵션을 나열하는 **쿼리** 를 제공해야 합니다. 화면에 반환해야 하는 필드가 제공됩니다. 이러한 필드는 배달 방법 및 보고서 매개 변수에 따라 달라집니다.  
  
최상의 결과를 얻으려면 데이터 기반 구독에 사용하기 전에 먼저 SQL Server Management Studio에서 쿼리를 실행합니다. 그러면 결과를 통해 필요한 정보가 포함되어 있는지 확인할 수 있습니다. 쿼리 결과에 대해 유의해야 할 중요한 점은 다음과 같습니다.  
  
-   결과 집합의 열은 배달 옵션 및 보고서 매개 변수에 지정할 수 있는 값을 결정합니다. 예를 들어 전자 메일 배달을 위한 데이터 기반 구독을 만드는 경우 전자 메일 주소 열이 있어야 합니다.  
  
-   결과 집합의 행은 생성되는 보고서 배달의 수를 결정합니다. 10,000개의 행이 있다면 보고서 서버는 10,000개의 알림 및 배달을 생성합니다.  
  
![ssRSWebPortal-subscriptions5](../reporting-services/media/ssrswebportal-subscriptions5.png)  
  
쿼리의 유효성을 검사할 수 있습니다. **쿼리 제한 시간**을 정의할 수도 있습니다.  
  
쿼리가 생성된 후 필수 필드에 값을 할당할 수 있습니다. 수동 데이터를 입력하거나 만든 데이터 집합에서 필드를 선택할 수 있습니다.

[웹 포털](../reporting-services/web-portal-ssrs-native-mode.md)  
[페이지를 매긴 보고서 사용](working-with-paginated-reports-web-portal.md)  
[공유 데이터 집합 작업](../reporting-services/work-with-shared-datasets-web-portal.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
