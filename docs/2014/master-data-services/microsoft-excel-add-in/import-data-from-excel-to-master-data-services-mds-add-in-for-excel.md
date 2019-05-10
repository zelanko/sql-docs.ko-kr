---
title: Excel에서 MDS (MDS 추가 기능 Excel 용)로 데이터 게시 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ffb122b96182b1079c95adf13d26c9a4949f6ddf
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65478801"
---
# <a name="publish-data-from-excel-to-mds-mds-add-in-for-excel"></a>Excel에서 MDS로 데이터 게시(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서는 Excel에서 작업을 마치고 다른 사용자가 데이터 액세스할 수 있도록 변경 내용을 저장하려는 경우 데이터를 MDS 리포지토리에 게시합니다.  
  
> [!NOTE]
>  -   변경 내용을 게시하면 MDS 관리 셀에 대한 주석이 삭제됩니다.  
> -   MDS 관리 셀에서는 수식을 사용할 수 없습니다. MDS 관리 셀의 수식은 텍스트 값으로 처리됩니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   활성 워크시트에는 MDS 관리 데이터가 포함되어야 하며, 사용자가 MDS 관리 데이터에서 항목을 변경했거나 추가했어야 합니다.  
  
-   멤버를 추가하는 경우 엔터티에 대한 코드를 자동으로 생성하는 경우 **코드** 값을 지정할 필요가 없습니다. 자세한 내용은 [코드 자동 생성&#40;Master Data Services&#41;](../automatic-code-creation-master-data-services.md)을 참조하세요.  
  
### <a name="to-publish-data-to-the-mds-repository"></a>MDS 저장소에 데이터를 게시하려면  
  
1.  **게시 및 유효성 검사** 그룹에서 **게시**를 클릭합니다.  
  
2.  (선택 사항) **게시 및 주석** 대화 상자가 표시되면 모든 업데이트에 대해 동일한 주석(설명)을 공유하거나 각 변경 내용에 대해 개별적으로 주석을 달도록 선택합니다.  
  
3.  (선택 사항) **이 대화 상자를 다시 표시 안 함** 확인란을 선택합니다. 이후에 언제라도 **설정** 을 선택하고 **게시할 때 게시 및 주석 대화 상자 표시** 확인란을 선택하여 대화 상자를 표시할 수 있습니다.  
  
4.  **게시**를 클릭합니다.  
  
> [!NOTE]  
>  워크시트에 새 멤버(행)를 추가하는 중이고 MDS 리포지토리에 성공적으로 게시할 수 없으면 사용자에게 워크시트에 있는 모든 특성에 대한 **업데이트** 권한이 없을 수 있습니다. **검토** 탭의 **변경 내용** 그룹에서 **시트 보호 해제** 를 클릭하여 다시 게시합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [비즈니스 규칙 적용&#40;Excel용 MDS 추가 기능&#41;](apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 게시 &#40;MDS 추가 기능에 Excel 용&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [데이터 유효성 검사&#40;Excel용 MDS 추가 기능&#41;](validating-data-mds-add-in-for-excel.md)  
  
  
