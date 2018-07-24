---
title: 특성 유형 변경(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3ed7a1d150b785bb6cd87a33b74121d1b598e390
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38059065"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>특성 유형 변경(Excel용 MDS 추가 기능)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 관리자는 허용되는 문자 개수 또는 데이터 형식이 잘못된 경우 특성 유형을 변경할 수 있습니다.  
  
 제한된 목록(도메인 기반 특성)을 만들도록 특성 유형을 변경하려는 경우 [도메인 기반 특성 만들기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)를 참조하세요.  
  
> [!NOTE]  
>  **이름** 또는 **코드** 열의 유형이나 길이는 업데이트할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 와 **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   기존 모델, 엔터티 및 특성이 있어야 합니다.  
  
### <a name="to-change-the-attribute-type"></a>특성 유형을 변경하려면  
  
1.  Excel에서 변경하려는 열(특성)이 포함된 엔터티를 로드합니다. 자세한 내용은 [Master Data Services에서 Excel로 데이터 내보내기](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)를 참조하세요.  
  
2.  변경할 열에서 셀을 클릭합니다.  
  
3.  **모델 작성** 그룹에서 **특성 속성**을 클릭합니다.  
  
4.  **특성 속성** 대화 상자에서 필요에 따라 설정을 업데이트합니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>특성 유형을 변경하면 어떻게 됩니까?  
 특성에 종속성이 존재하여, 그러한 속성이 MDS 비즈니스 규칙 또는 파생 계층에서 참조되는 경우 특성의 데이터 형식을 변경할 수 없습니다. 특성 유형을 개체에서 참조하기 때문에 수정할 수 없다는 오류가 발생합니다.  
  
 특성 값에 대한 데이터 형식을 변환하는 동안 오류가 있으면 MDS는 다음을 수행합니다.  
  
-   특성의 데이터 형식을 변경합니다.  
  
-   이전 값을 가진 “_old” 접미사를 사용해서 특성의 복사본을 생성합니다. 이를 사용되지 않는 특성이라고 부릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [특성&#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)   
 [모델 작성&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  
