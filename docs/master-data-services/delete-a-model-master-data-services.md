---
title: 모델 삭제
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting models [Master Data Services]
- models [Master Data Services], deleting models
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7badbd43fd526ff66b599f04e6aeb36443cd3684
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811546"
---
# <a name="delete-a-model-master-data-services"></a>모델 삭제(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델과 모든 관련 데이터를 제거하려면 모델을 삭제합니다.  
  
> [!NOTE]  
>  이 절차를 완료하면 모든 모델 버전의 모든 개체와 데이터가 영구적으로 삭제됩니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
### <a name="to-delete-a-model"></a>모델을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **모델**을 클릭합니다.  
  
3.  **모델 관리** 페이지의 표에서 삭제할 모델의 행을 선택합니다.  
  
4.  **삭제**를 클릭합니다.  
  
5.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
6.  추가 확인 대화 상자에서 **확인**을 클릭합니다.  
  
 표의 **상태** 열에는 모델에 대한 작업의 상태가 표시됩니다. **모델 저장** 단추를 클릭 하면 모델이 업데이트 중임을 나타내는 ![업데이트](../master-data-services/media/mds-model-status-updating.png "업데이트") 이미지가 표시 됩니다. 모델을 만들거나 편집할 때 오류가 발생 하면 ![오류](../master-data-services/media/mds-model-status-error.png "오류") 이미지가 표시 됩니다. 오류가 발생하지 않는 경우 모델은 정상 상태가 되며 ![확인](../master-data-services/media/mds-model-status-ok.png "확인") 이미지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [모델 &#40;MDS(Master Data Services)&#41;](../master-data-services/models-master-data-services.md)   
 [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)  
  
  
