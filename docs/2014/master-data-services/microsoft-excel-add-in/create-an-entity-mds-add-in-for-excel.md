---
title: 엔터티 만들기(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: d354abb3-88fe-4b40-a374-f6256b84ffae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: de753f0aa019e6cee4eab30076205dc42d1a2c04
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065373"
---
# <a name="create-an-entity-mds-add-in-for-excel"></a>엔터티 만들기(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 관리자는 새 엔터티를 만들어 데이터를 저장할 수 있습니다. 엔터티를 만들 때 엔터티에 저장할 데이터의 샘플을 로드해야 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 와 **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../administrators-master-data-services.md)를 참조하세요.  
  
-   만든 엔터티를 포함할 기존 모델이 있어야 합니다. 자세한 내용은 [모델 만들기&#40;Master Data Services&#41;](../create-a-model-master-data-services.md)를 참조하세요.  
  
-   데이터가 다음 요구 사항을 충족해야 합니다.  
  
    -   데이터에 머리글 행이 있어야 합니다.  
  
    -   **이름** 및 **코드** 열을 포함하는 것이 좋습니다. **코드** 는 각 행의 고유 식별자입니다.  
  
    -   머리글 행 외에도 데이터 행이 하나 이상 있어야 합니다. 모든 열에 값이 포함되어 있을 필요는 없지만 엔터티에 포함할 데이터를 잘 나타내는 데이터가 있어야 합니다.  
  
    -   고유 식별자(MDS에서는 **코드**라고 함)가 포함된 열이 있는 경우 값이 고유해야 합니다. 식별자가 포함된 열이 없으면 엔터티를 만들 때 자동으로 생성되도록 할 수 있습니다.  
  
    -   수식이 포함된 셀이 없어야 합니다.  
  
    -   시간 값이 포함된 셀이 없어야 합니다. MDS에서 날짜 값은 저장할 수 있지만 시간 값은 저장할 수 없습니다.  
  
### <a name="to-create-an-entity-and-load-data"></a>엔터티를 만들고 데이터를 로드하려면  
  
1.  로드할 데이터가 들어 있는 Excel 워크시트를 열거나 만듭니다.  
  
2.  새 엔터티에 로드할 셀을 선택합니다.  
  
3.  **마스터 데이터** 탭의 **모델 작성** 그룹에서 **엔터티 만들기**를 클릭합니다.  
  
4.  MDS 저장소에 연결할지 묻는 메시지가 표시되면 연결합니다.  
  
5.  **엔터티 만들기** 대화 상자에서 기본 범위를 그대로 적용하거나 로드할 데이터에 맞게 변경합니다.  
  
6.  **내 데이터에 머리글 표시** 확인란의 선택을 취소하지 마십시오.  
  
7.  **모델** 목록에서 모델을 선택합니다.  
  
8.  **버전** 목록에서 버전을 선택합니다.  
  
9. **새 엔터티 이름** 상자에 엔터티의 이름을 입력합니다.  
  
10. **코드** 목록에서 고유 식별자가 포함된 열을 선택하거나 코드가 자동으로 생성되도록 둡니다.  
  
11. (선택 사항) **이름** 목록에서 각 멤버의 이름이 포함된 열을 선택합니다.  
  
12. **확인**을 클릭합니다. 엔터티가 만들어지면 새 머리글 행이 표시되고 셀이 강조 표시되며 엔터티 이름과 일치하도록 시트 이름이 업데이트됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   발생한 오류를 보려면 **게시 및 유효성 검사** 그룹에서 **상태 표시**를 클릭합니다. ValidationStatus 및 InputStatus 열이 표시됩니다. 자세한 내용은 [데이터 유효성 검사&#40;Excel용 MDS 추가 기능&#41;](validating-data-mds-add-in-for-excel.md)를 참조하세요.  
  
-   예상한 데이터 형식으로 특성이 만들어졌는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [도메인 기반 특성 만들기&#40;Excel용 MDS 추가 기능&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)  
  
  
