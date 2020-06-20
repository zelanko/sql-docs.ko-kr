---
title: 큐브 뷰 만들기 및 관리 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.perspectivedb.f1
ms.assetid: 2a411c2b-2820-4086-ad7f-ce6a941fefc7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 51ba015363cafee537f6845ec2039dba6027e6ec
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939794"
---
# <a name="create-and-manage-perspectives-ssas-tabular"></a>큐브 뷰 만들기 및 관리(SSAS 테이블 형식)
  큐브 뷰는 모델을 비즈니스 또는 애플리케이션 중심의 관점에서 파악할 수 있게 해주는 보기 가능한 모델 하위 집합을 정의합니다. 이 항목의 태스크에서는 모델 디자이너의 **큐브 뷰** 를 사용하여 큐브 뷰를 만들고 관리하는 방법을 설명합니다.  
  
 이 항목에는 다음 태스크가 포함됩니다.  
  
-   [큐브 뷰를 추가 하려면](#bkmk_add)  
  
-   [큐브 뷰를 편집하려면](#bkmk_edit)  
  
-   [큐브 뷰의 이름을 바꾸려면](#bkmk_rename)  
  
-   [큐브 뷰를 삭제하려면](#bkmk_delete)  
  
-   [큐브 뷰를 복사하려면](#bkmk_copy)  
  
## <a name="tasks"></a>작업  
 큐브 뷰를 만들려면 **큐브 뷰** 대화 상자를 사용합니다. 이 대화 상자에서는 큐브 뷰를 추가, 편집, 삭제, 복사 및 확인할 수 있습니다. **큐브 뷰** 대화 상자를 보려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **모델** 메뉴에서 **큐브 뷰**를 클릭합니다.  
  
###  <a name="to-add-a-perspective"></a><a name="bkmk_add"></a> 큐브 뷰를 추가하려면  
  
-   새 큐브 뷰를 추가하려면 **새 큐브 뷰**를 클릭합니다. 그런 다음 포함할 필드 개체를 선택하거나 선택 취소하고 새 큐브 뷰의 이름을 지정합니다.  
  
     모든 필드 개체를 선택 취소하고 빈 큐브 뷰를 만들면 사용자가 이 큐브 뷰를 사용할 때 빈 필드 목록이 표시됩니다. 큐브 뷰에는 하나 이상의 테이블 및 열을 포함해야 합니다.  
  
###  <a name="to-edit-a-perspective"></a><a name="bkmk_edit"></a>큐브 뷰를 편집 하려면  
  
-   큐브 뷰를 수정 하려면 큐브 뷰 열에서 필드를 선택 하 고 선택 취소 합니다. 그러면 큐브 뷰에서 필드 개체가 추가 되거나 제거 됩니다.  
  
###  <a name="to-rename-a-perspective"></a><a name="bkmk_rename"></a>큐브 뷰의 이름을 바꾸려면  
  
-   큐브 뷰 열 머리글 (큐브 뷰 이름) 위로 마우스를 가져가면 **이름 바꾸기** 단추가 나타납니다. 큐브 뷰의 이름을 바꾸려면 **이름 바꾸기**를 클릭하고 새 이름을 입력하거나 기존 이름을 편집합니다.  
  
###  <a name="to-delete-a-perspective"></a><a name="bkmk_delete"></a>큐브 뷰를 삭제 하려면  
  
-   큐브 뷰 열 머리글 (큐브 뷰 이름) 위로 마우스를 이동 하면 **삭제** 단추가 나타납니다. 큐브 뷰를 삭제하려면 **삭제** 단추를 클릭하고 확인 창에서 **예** 를 클릭합니다.  
  
###  <a name="to-copy-a-perspective"></a><a name="bkmk_copy"></a>큐브 뷰를 복사 하려면  
  
-   큐브 뷰 열 머리글을 마우스로 가리키면 **복사** 단추가 나타납니다. 큐브 뷰의 복사본을 만들려면 **복사** 단추를 클릭합니다. 그러면 선택한 큐브 뷰의 복사본이 기존 큐브 뷰의 오른쪽에 새 큐브 뷰로 추가됩니다. 새 큐브 뷰는 복사 원본 큐브 뷰의 이름을 상속하며, 이름 끝에 *- 복사본* 이라는 주석이 추가됩니다. 예를 들어 *sales* 큐브 뷰의 복사본을 만드는 경우 새 큐브 뷰를 *판매 복사본*이라고 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSAS 테이블 형식&#41;&#40;큐브 뷰](perspectives-ssas-tabular.md)   
 [계층 구조&#40;SSAS 테이블 형식&#41;](hierarchies-ssas-tabular.md)  
  
  
