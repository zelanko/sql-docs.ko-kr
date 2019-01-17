---
title: 구독 뷰를 만들어 데이터 내보내기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f9619bca36ec488fdd5e25b5b9eb9a82370d7049
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754675"
---
# <a name="create-a-subscription-view-to-export-data-master-data-services"></a>구독 뷰를 만들어 데이터 내보내기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  구독 뷰를 만들어 구독 시스템으로 Master Data Services 데이터를 내보낼 수 있습니다. 그러면 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 데이터의 뷰가 생성됩니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **통합 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
### <a name="to-create-and-edit-a-subscription-view"></a>구독 뷰를 만들고 편집하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **통합 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **뷰 만들기**를 클릭합니다.  
  
3.  **구독 뷰** 페이지에서 보기를 만들려면 **추가** 를 클릭하고 보기를 편집하려면 **편집** 을 클릭합니다. 그러면 오른쪽에 패널이 표시됩니다.  
  
4.  **구독 뷰 만들기** 창의 **이름** 상자에 뷰의 이름을 입력합니다.  
  
     **구독 뷰 편집** 창의 **이름** 상자에 업데이트된 뷰의 이름을 입력합니다.  
  
5.  **모델** 목록에서 모델을 선택합니다.  
  
6.  일시 삭제된 멤버를 뷰에 포함하려면 **일시 삭제된 멤버 포함**을 선택합니다.  
  
7.  **버전 옵션** 에서 **버전** 또는 **버전 플래그**를 선택하고 해당하는 목록에서 옵션을 선택합니다.  
  
    > [!TIP]  
    >  버전 플래그를 기반으로 구독 뷰를 만듭니다. 버전을 잠그는 경우에는 구독 뷰를 업데이트하지 않고 플래그를 열린 버전에 다시 할당할 수 있습니다.  
  
8.  **데이터 원본** 옵션에서 **엔터티** 또는 **파생 계층** 을 선택하고 해당하는 목록에서 옵션을 선택합니다.  
  
9. **형식** 목록에서 구독 뷰 형식을 선택합니다.  
  
10. **형식** 목록에서 **명시적 수준** 또는 **파생 수준** 을 선택한 경우에는 뷰에 포함할 계층의 수준 수를 입력합니다.  
  
11. **저장**을 클릭합니다.  
  
## <a name="view-information"></a>뷰 정보  
 생성되는 각 뷰에 대해 열이 10개 포함된 행이 표에 추가됩니다. 다음 표에서는 열을 설명합니다.  
  
|Column|설명|  
|------------|-----------------|  
|상태|보기 상태입니다.<br /><br /> **저장**을 클릭하면 뷰가 업데이트 중임을 나타내는 ![상태 업데이트 아이콘](../master-data-services/media/mds-statusicon-updating.png "상태 업데이트 아이콘") 이미지가 표시됩니다.<br /><br /> 뷰를 만들거나 편집할 때 오류가 발생하면 ![오류 상태 아이콘](../master-data-services/media/mds-statusicon-error.png "오류 상태 아이콘") 이미지가 표시됩니다.<br /><br /> 그렇지 않으면 상태가 정상이고 ![정상 상태 아이콘](../master-data-services/media/mds-statusicon-ok.png "정상 상태 아이콘")이미지가 표시됩니다.|  
|속성|구독 뷰 이름입니다.|  
|Model|모델 이름입니다.|  
|버전 옵션|버전 이름입니다.|  
|버전|버전 플래그 이름입니다.|  
|엔터티|파생 계층 이름입니다.|  
|데이터 원본|엔터티 이름입니다.|  
|형식|뷰의 데이터 형식을 지정합니다.|  
|Level|명시적 수준 또는 파생 수준 뷰 형식에만 사용되는 뷰의 수준 수를 지정합니다.|  
|삭제된 멤버 포함|일시 삭제된 멤버가 뷰에 포함되는지 여부를 나타냅니다.|  
  
 뷰를 클릭하면 다음 정보가 표시됩니다.  
  
-   **만든 사람**: 보기를 만든 사용자의 이름입니다.  
  
-   **On**: 보기를 만든 날짜와 시간입니다.  
  
-   **업데이트한 사람**: 보기를 마지막으로 업데이트한 사용자의 이름입니다.  
  
-   **On**: 보기를 마지막으로 업데이트한 날짜와 시간입니다.  
  
## <a name="see-also"></a>참고 항목  
 [개요: 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [구독 뷰 삭제&#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [버전 플래그 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  
