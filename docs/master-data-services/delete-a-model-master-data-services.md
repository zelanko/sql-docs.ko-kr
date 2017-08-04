---
title: "모델 (Master Data Services)를 삭제 합니다. | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting models [Master Data Services]
- models [Master Data Services], deleting models
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be50aa7e9de502b0db2cb427bf894081196b579e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="delete-a-model-master-data-services"></a>모델 삭제(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델과 모든 관련 데이터를 제거하려면 모델을 삭제합니다.  
  
> [!NOTE]  
>  이 절차를 완료하면 모든 모델 버전의 모든 개체와 데이터가 영구적으로 삭제됩니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-delete-a-model"></a>모델을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **모델**을 클릭합니다.  
  
3.  **모델 관리** 페이지의 표에서 삭제할 모델의 행을 선택합니다.  
  
4.  **삭제**를 클릭합니다.  
  
5.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
6.  추가 확인 대화 상자에서 **확인**을 클릭합니다.  
  
 표의 **상태** 열에는 모델에 대한 작업의 상태가 표시됩니다. 클릭할 때는 **모델 저장** 단추는 ![업데이트](../master-data-services/media/mds-model-status-updating.png "업데이트") 모델 업데이트 되 고 있음을 나타내는 이미지가 표시 됩니다. 작성 하거나 모델을 편집할 때 오류가 있는 경우는 ![오류](../master-data-services/media/mds-model-status-error.png "오류") 이미지가 표시 됩니다. 오류가 발생하지 않으면 상태가 정상이며 ![확인](../master-data-services/media/mds-model-status-ok.png "확인") 이미지가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [모델 &#40; Master Data services&#41;](../master-data-services/models-master-data-services.md)   
 [모델 &#40; 만들기 Master Data services&#41;](../master-data-services/create-a-model-master-data-services.md)  
  
  
