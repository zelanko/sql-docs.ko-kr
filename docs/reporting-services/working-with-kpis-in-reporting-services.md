---
title: "Reporting Services에서 Kpi 사용 | Microsoft Docs"
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a28cf500-6d47-4268-a248-04837e7a09eb
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: f8057d09bb9118ef5575645f3fab9ba7a1fede94
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---

# <a name="working-with-kpis-in-reporting-services"></a>Reporting Services에서 KPI 사용

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

핵심 성과 지표(KPI)는 목표에 대한 진척 정도를 알려 주는 시각적 단서입니다.  핵심 성과 지표는 팀, 관리자 및 비즈니스에서 측정 가능한 목표에 대한 진척 정도를 빠르게 평가하는 데 있어 중요합니다.   
  
SQL Server 2016 Reporting Services에서 KPI를 사용하여 다음 질문에 대한 답변을 쉽게 시각화할 수 있습니다.  
  
-   내 앞 또는 뒤에 있는 것은 무엇인가?  
  
-   나는 얼마나 앞 또는 뒤에 있는가?  
  
-   내가 완료한 최소는 무엇인가?  
  
## <a name="creating-a-dataset"></a>데이터 집합 만들기  
KPI는 공유된 데이터 집합에서 데이터의 첫 행만 사용합니다. 사용하려는 데이터가 첫 행에 있는지 확인합니다. 공유 데이터 집합을 만들기 위해 보고서 작성기 또는 SQL Server Data Tools를 사용할 수 있습니다.  
  
> **참고**: 데이터 집합은 KPI와 같은 폴더에 있이 필요가 없습니다.  
  
## <a name="placement-of-kpis"></a>KPI의 배치  
  
KPI는 보고서 서버의 모든 폴더에서 만들 수 있습니다.  KPI를 만들기 전에 저장할 적합한 위치에 대해 생각해 봐야 할 것입니다. 다른 보고서, KPI에 상대적으로 동시에 다른 사람에게 공개되는 폴더에 놓기를 원할 수 있습니다.  
  
## <a name="adding-a-kpi"></a>KPI 추가  
  
KPI의 위치를 확인한 후 해당 폴더로 이동하고 상단 메뉴에서 **New(새로 만들기)** > **KPI** 를 선택합니다.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
**New KPI(새 KPI)** 화면이 나타납니다.  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
정적 값을 할당 하거나 공유 데이터 집합에서 데이터를 사용할 수 있습니다. 새 KPI를 만들 때 임의 수동 데이터 집합으로 채워집니다.  
  
|필드|Description|  
|---|---|  
|값 형식|  표시되는 값의 형식을 변경하는 데 사용합니다.|   
|값|KPI에 대해 표시할 값입니다.|  
|목표|숫자 값에 대한 비교로 사용되며 백분율 차로 표시됩니다.|  
|상태|KPI 타일 색을 결정하는 데 사용되는 숫자 값입니다. 유효한 값은 1(녹색), 0(주황색) 및 -1(빨강)입니다.|  
|추세 집합|차트 시각화에 사용되는 쉼표로 구분되는 숫자 값입니다. 또한, 추세를 나타내는 값으로 데이터 집합의 열에 설정할 수도 있습니다.|  
  
> **경고**: 설계 시간에 **상태** 필드에 대한 단어 값을 사용할 수 있지만, 데이터 집합을 새로 고침하는 경우 숫자 값을 사용해야 합니다. 숫자 대신 단어 값으로 데이터 집합을 새로 고침할 경우 서버에서 KPI가 손상될 수 있습니다.  
  
> **참고**: **값**, **목표** 및 **상태** 필드는 데이터 집합 결과의 첫 행에서만 값을 선택할 수 있습니다. 하지만, **집합 추세** 필드는 추세를 반영하는 열을 선택할 수 있습니다.  
  
공유 데이터 집합에서 데이터를 사용하기 위해 다음을 수행할 수 있습니다.  
  
1.  필드 드롭다운 상자를 **수동으로 설정**, 또는 **설정 안 함**에서 **데이터 집합 필드**로 변경합니다.  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2.  선택 된 **줄임표 (...)**  데이터 상자에 있습니다. 그러면 **데이터 집합 선택** 화면이 나타납니다.  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3.  표시하려는 데이터가 있는 데이터 집합을 선택합니다.  
  
4.  사용하려는 필드를 선택합니다. **확인**을 선택합니다.  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5.  **값 형식** 을 값 형식에 맞게 변경합니다. 이 예제에서는 값은 통화입니다.  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6.  **적용**을 선택합니다.  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)  
  
## <a name="removing-a-kpi"></a>KPI 제거  
  
KPI를 제거하기 위해 다음을 수행할 수 있습니다.  
  
1.  선택 된 **줄임표 (...)**  제거 하려는 KPI의 합니다. **관리**를 선택합니다.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2.  **삭제**를 선택합니다. 확인 대화 상자에서 **삭제** 를 다시 선택합니다.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>KPI 새로 고침  
  
KPI를 새로 고치려면 공유 데이터 집합에 대 한 캐싱을 구성 해야 합니다. 새로 고침 계획을 캐시에 대 한 자세한 내용은 참조 하십시오. [공유 데이터 집합 작업을](../reporting-services/work-with-shared-datasets-web-portal.md)합니다.  
  
## <a name="next-steps"></a>다음 단계
  
[웹 포털](../reporting-services/web-portal-ssrs-native-mode.md)  
[공유 데이터 집합 작업](../reporting-services/work-with-shared-datasets-web-portal.md)

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
