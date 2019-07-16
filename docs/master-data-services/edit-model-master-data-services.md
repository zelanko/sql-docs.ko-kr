---
title: 모델 편집(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], changing name
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0eb25db76d1dd14d3eb715072683ee8c046c392b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052070"
---
# <a name="edit-model-master-data-services"></a>모델 편집(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 모델의 이름과 설명을 변경하고 트랜잭션 로그를 보존할 기간(일)을 지정할 수 있습니다.  
  
 자세한 내용은 [트랜잭션&#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)을 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-change-a-model"></a>모델을 변경하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **모델**을 클릭합니다.  
  
3.  **모델 관리** 페이지의 표에서 이름이나 설명을 변경할 모델의 행을 선택합니다.  
  
4.  **편집**을 클릭합니다.  
  
5.  **이름** 상자에 모델의 업데이트된 이름을 입력합니다.  
  
6.  **설명** 필드에 모델의 업데이트된 설명을 입력합니다.  
  
7.  **로그 보존 기간(일)** 필드에서 로그 데이터 보존 옵션 중 하나를 선택합니다. 기본값인 **시스템 설정**은 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 시스템 설정에서 값이 상속됨을 나타냅니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
     시스템 설정을 재정의하고 트랜잭션 로그 데이터는 제거하지 않으려면 **아니요**를 선택합니다. 해당일의 로그 데이터만 보존하고 이전 날짜의 모든 로그 데이터를 자르려면 **예**를 선택하고 **일** 필드의 값을 0으로 설정합니다. 지정된 기간(일) 동안 로그 데이터를 보존하려면 **예** 를 선택하고 **일** 필드의 값을 원하는 기간(일)으로 설정합니다.  
  
8.  **모델 저장**을 클릭합니다.  
  
 표의 **상태** 열에는 모델에 대한 작업의 상태가 표시됩니다. **모델 저장** 단추를 클릭하면 모델을 업데이트하는 중임을 나타내는 ![업데이트 중](../master-data-services/media/mds-model-status-updating.png "업데이트 중") 이미지가 표시됩니다. 모델을 만들거나 편집할 때 오류가 발생하면 ![오류](../master-data-services/media/mds-model-status-error.png "오류") 이미지가 표시됩니다. 오류가 발생하지 않으면 상태가 정상이며 ![확인](../master-data-services/media/mds-model-status-ok.png "확인") 이미지가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [모델 삭제&#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [모델&#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
  
