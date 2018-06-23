---
title: 표시기 아이콘 및 표시기 집합 변경(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8a056adf-4473-473d-9b0c-314675af7bfd
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: d681a7b5e9c72283d924970d843582bb82b8522c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187347"
---
# <a name="change-indicator-icons-and-indicator-sets-report-builder-and-ssrs"></a>표시기 아이콘 및 표시기 집합 변경(보고서 작성기 및 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 수 항상 데이터를 효율적으로 나타내고 전달된 된 보고서에서 잘 작동 하는 미리 구성 된 표시기 집합이 제공 합니다. 이 항목에서는 표시기 아이콘 모양을 변경하고 더 많거나 더 적은 표시기 아이콘 또는 다른 표시기 아이콘을 포함하도록 표시기 집합을 변경하는 절차에 대해 설명합니다.  
  
 식을 사용하여 색 등의 옵션을 설정할 수 있습니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-color-of-an-indicator-icon"></a>표시기 아이콘의 색을 변경하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  변경할 아이콘 옆의 **색** 열에 있는 아래쪽 화살표를 클릭하고 사용할 색, **색 없음**또는 **다른 색**을 클릭합니다.  
  
     필요한 경우 **식** 단추(*fx*)를 클릭하여 **색** 옵션의 값을 설정하는 식을 편집합니다.  
  
     **다른 색**을 클릭한 경우 **색 선택** 대화 상자가 열리고 여기서 여러 색 중 원하는 색을 선택할 수 있습니다. 해당 옵션에 대한 자세한 내용은 [색 선택 대화 상자&#40;보고서 작성기 및 SSRS&#41;](../select-color-dialog-box-report-builder-and-ssrs.md)를 참조하세요. **확인** 을 클릭하여 **색 선택** 대화 상자를 닫습니다.  
  
4.  **확인**을 클릭합니다.  
  
### <a name="to-change-the-icon"></a>아이콘을 변경하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  변경할 아이콘 옆의 아래쪽 화살표를 클릭하고 다른 아이콘을 선택합니다.  
  
     필요한 경우 **식** 단추(*fx*)를 클릭하여 **아이콘** 옵션의 값을 설정하는 식을 편집합니다.  
  
4.  **확인**을 클릭합니다.  
  
### <a name="to-use-a-custom-image-as-an-indicator-icon"></a>사용자 지정 이미지를 표시기 아이콘으로 사용하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  변경할 아이콘 옆의 아래쪽 화살표를 클릭하고 **이미지**를 선택합니다.  
  
4.  **이미지 원본 선택** 목록에서 **외부**, **포함**또는 **데이터베이스**를 선택합니다.  
  
5.  이미지 원본에 따라 다음 중 하나를 수행합니다.  
  
    -   보고서 외부에 저장된 이미지를 사용하려면 **찾아보기** 를 클릭하고 이미지를 찾습니다. 보고서에는 이미지에 대한 참조가 포함됩니다.  
  
    -   보고서에 포함된 이미지를 사용하려면 **가져오기** 를 클릭하고 이미지를 찾습니다. 이미지가 보고서 정의에 추가되며 정의와 함께 저장됩니다.  
  
    -   데이터베이스에 있는 이미지를 사용하려면 **이 필드 사용** 목록에서 필드를 선택하고 **이 MIME 형식 사용** 목록에서 이미지의 MIME 형식을 선택합니다.  
  
6.  **확인**을 클릭합니다.  
  
### <a name="to-add-an-icon-to-the-indicator-set"></a>표시기 집합에 아이콘을 추가하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  **추가**를 클릭합니다. 기본 아이콘과 **색 없음** 옵션을 사용하여 표시기가 추가됩니다.  
  
     원하는 아이콘과 색을 사용하도록 표시기를 구성합니다. 이 작업을 수행하는 단계는 이 항목 앞부분의 절차에 설명되어 있습니다.  
  
4.  **확인**을 클릭합니다.  
  
### <a name="to-delete-an-icon-to-the-indicator-set"></a>표시기 집합에서 아이콘을 삭제하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  삭제할 아이콘을 선택하고 **삭제**를 클릭합니다.  
  
4.  **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [표시기&#40;보고서 작성기 및 SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  