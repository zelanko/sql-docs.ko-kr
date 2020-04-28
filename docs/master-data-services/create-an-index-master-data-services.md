---
title: 인덱스 만들기
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d694a105-69b1-4ff6-99d3-1f408b916b81
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a18de9c33def5b0603f4460f87e7c5589ead4521
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728425"
---
# <a name="create-an-index-master-data-services"></a>인덱스 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  쿼리 성능을 개선하려면 자주 쿼리하는 특성 목록에 대해 사용자 지정 인덱스를 만듭니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 절차를 수행하려면  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
 **인덱스를 만들려면**  
  
1.  마스터 데이터 관리자에서 **시스템 관리자**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지의 **표** 에서 인덱스를 만들려는 엔터티의 행을 선택합니다.  
  
4.  **인덱스**를 클릭합니다.  
  
5.  **이름** 상자에 인덱스의 이름을 입력합니다.  
  
6.  고유한 인덱스를 만들려면 **고유** 를 선택합니다. 인덱스 유형에 대한 자세한 내용은 [사용자 지정 인덱스&#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)을 참조하세요.  
  
7.  **사용 가능한 특성** 상자의 특성을 클릭하고 **추가** 화살표를 클릭합니다. 모든 특성을 추가하려면 **모두 추가** 화살표를 클릭합니다.  
  
8.  **저장**을 클릭합니다.  
  
 생성되는 각 인덱스에 대해 열이 4개 포함된 행이 표에 추가됩니다. 다음 표에서는 열을 설명합니다.  
  
|열 이름|설명|  
|-----------------|-----------------|  
|상태|인덱스 상태입니다.<br /><br /> **저장**을 클릭 하면 인덱스가 업데이트 중임을 나타내는 ![상태 업데이트 이미지 아이콘이](../master-data-services/media/mds-statusicon-updating.png "상태 업데이트 아이콘") 표시 됩니다.<br /><br /> 인덱스를 만들거나 편집할 때 오류가 발생 하면 ![오류 상태 이미지 아이콘이](../master-data-services/media/mds-statusicon-error.png "오류 상태 아이콘") 표시 됩니다.<br /><br /> 그렇지 않으면 상태가 정상 이며 ![ok 상태 이미지 아이콘이](../master-data-services/media/mds-statusicon-ok.png "정상 상태 아이콘") 표시 됩니다.|  
|Name|인덱스 이름입니다.|  
|고유|인덱스가 고유한지 여부를 지정합니다.|  
|대상 특성|인덱스를 정의한 특성의 표시 이름을 표시합니다.|  
  
 인덱스를 클릭하면 다음 정보가 표시됩니다.  
  
-   **만든 사람**: 인덱스를 만든 사용자의 이름입니다.  
  
-   **날짜**: 인덱스를 만든 날짜와 시간입니다.  
  
-   **업데이트한 사람**: 인덱스를 마지막으로 업데이트한 사용자의 이름입니다.  
  
-   **날짜**: 인덱스를 마지막으로 업데이트한 날짜와 시간입니다.  
  
## <a name="next-steps"></a>다음 단계  
 [인덱스 편집 및 삭제&#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 인덱스&#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)  
  
  
