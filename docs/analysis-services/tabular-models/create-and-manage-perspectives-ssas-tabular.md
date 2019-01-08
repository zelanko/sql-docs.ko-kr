---
title: Analysis Services 테이블 형식 모델의 큐브 뷰를 만들고 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 962b6b90de6d95107d1a4cdd3484a44205afb630
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071850"
---
# <a name="create-and-manage-perspectives"></a>큐브 뷰를 만들고 설정 합니다. 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  큐브 뷰는 모델을 비즈니스 또는 애플리케이션 중심의 관점에서 파악할 수 있게 해주는 보기 가능한 모델 하위 집합을 정의합니다. 이 항목의 태스크에서는 모델 디자이너의 **큐브 뷰** 를 사용하여 큐브 뷰를 만들고 관리하는 방법을 설명합니다.  
  
## <a name="tasks"></a>태스크  
 큐브 뷰를 만들려면 **큐브 뷰** 대화 상자를 사용합니다. 이 대화 상자에서는 큐브 뷰를 추가, 편집, 삭제, 복사 및 확인할 수 있습니다. **큐브 뷰** 대화 상자를 보려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **모델** 메뉴에서 **큐브 뷰**를 클릭합니다.  
  
###  <a name="bkmk_add"></a> 큐브 뷰를 추가하려면  
  
-   새 큐브 뷰를 추가하려면 **새 큐브 뷰**를 클릭합니다. 그런 다음 포함할 필드 개체를 선택하거나 선택 취소하고 새 큐브 뷰의 이름을 지정합니다.  
  
     모든 필드 개체를 선택 취소하고 빈 큐브 뷰를 만들면 사용자가 이 큐브 뷰를 사용할 때 빈 필드 목록이 표시됩니다. 큐브 뷰에는 하나 이상의 테이블 및 열을 포함해야 합니다.  
  
###  <a name="bkmk_edit"></a> 큐브 뷰를 편집하려면  
  
-   큐브 뷰를 수정 하려면 확인 하 고 추가 하 고 필드 개체가 큐브 뷰에서 제거 하는 큐브 뷰 열에 필드의 선택을 취소 합니다.  
  
###  <a name="bkmk_rename"></a> 큐브 뷰의 이름을 바꾸려면  
  
-   큐브 뷰 열 머리글 (큐브 뷰의 이름)을 마우스로 가리키면 합니다 **이름 바꾸기** 단추가 나타납니다. 큐브 뷰의 이름을 바꾸려면 **이름 바꾸기**를 클릭하고 새 이름을 입력하거나 기존 이름을 편집합니다.  
  
###  <a name="bkmk_delete"></a> 큐브 뷰를 삭제하려면  
  
-   큐브 뷰 열 머리글 (큐브 뷰의 이름)을 마우스로 가리키면 합니다 **삭제** 단추가 나타납니다. 큐브 뷰를 삭제하려면 **삭제** 단추를 클릭하고 확인 창에서 **예** 를 클릭합니다.  
  
###  <a name="bkmk_copy"></a> 큐브 뷰를 복사하려면  
  
-   큐브 뷰 열 머리글을 가리키면 합니다 **복사** 단추가 나타납니다. 큐브 뷰의 복사본을 만들려면 **복사** 단추를 클릭합니다. 그러면 선택한 큐브 뷰의 복사본이 기존 큐브 뷰의 오른쪽에 새 큐브 뷰로 추가됩니다. 새 큐브 뷰는 복사 원본 큐브 뷰의 이름을 상속하며, 이름 끝에 *- 복사본* 이라는 주석이 추가됩니다. 예를 들어, 복사본을 *Sales* 큐브 뷰를 만든, 새 큐브 뷰의 이름은 *Sales-복사본*합니다.  
  
## <a name="see-also"></a>참고자료  
 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [계층 구조](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
