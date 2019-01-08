---
title: 유사한 데이터 일치(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f6fd6fc1-3569-42a5-b6cb-87a921c88f3b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 998588401c477d1a2022bdd7d19965c9c74ea2fa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760405"
---
# <a name="match-similar-data-mds-add-in-for-excel"></a>유사한 데이터 일치(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 DQS(Data Quality Services) 기능을 사용하여 데이터의 유사성을 찾을 수 있습니다.  
  
 이 절차를 수행하기 위해 다음 작업을 수행할 수 있습니다.  
  
-   기본 Data Quality Services 기술 자료를 사용합니다. 또는  
  
-   고유의 사용자 지정 DQS 기술 자료 및 일치 정책을 만듭니다. 자세한 내용은 [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md)를 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   MDS 관리 데이터가 포함된 워크시트가 있어야 합니다. 자세한 내용은 [Excel에 MDS에서 데이터 로드](export-data-to-excel-from-master-data-services.md)합니다.  
  
-   (선택 사항) 유사성을 검사하기 전에 다른 데이터와 MDS 관리 데이터를 결합할 수 있습니다. 자세한 내용은 [데이터 결합&#40;Excel용 MDS 추가 기능&#41;](combine-data-mds-add-in-for-excel.md)를 참조하십시오.  
  
### <a name="to-find-similarities-by-using-the-default-knowledge-base"></a>기본 기술 자료를 사용하여 유사성을 찾으려면  
  
1.  MDS 관리 데이터가 포함된 워크시트의 **데이터 품질** 그룹에서 **데이터 일치**를 클릭합니다.  
  
2.  **데이터 일치** 대화 상자의 **DQS 기술 자료** 목록에서 **DQS 데이터(기본값)** 를 선택합니다.  
  
3.  대화 상자에서 일치시킬 데이터가 포함된 각 열에 대해 행을 하나씩 추가합니다. 이 대화 상자의 필드에 대한 자세한 내용은 [How to Set Matching Rule Parameters](../../data-quality-services/create-a-matching-policy.md#MatchingRules)을 참조하십시오.  
  
4.  모든 가중치 값의 합계가 100%이면 **확인**을 클릭합니다.  
  
### <a name="to-find-similarities-by-using-a-custom-knowledge-base"></a>사용자 지정 기술 자료를 사용하여 유사성을 찾으려면  
  
1.  MDS 관리 데이터가 포함된 워크시트의 **데이터 품질** 그룹에서 **데이터 일치**를 클릭합니다.  
  
2.  **DQS 기술 자료** 목록에서 사용자 지정 기술 자료의 이름을 선택합니다.  
  
3.  워크시트의 각 열에 대해 DQS 도메인을 선택합니다.  
  
4.  모든 DQS 도메인을 워크시트의 열에 매핑했으면 **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   추가 정보를 보고 어떤 데이터가 비슷한지 결정합니다. 자세한 내용은 [데이터 품질 일치 열&#40;Excel용 MDS 추가 기능&#41;](data-quality-matching-columns-mds-add-in-for-excel.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Excel용 MDS 추가 기능의 데이터 품질 일치](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [데이터 일치](../../data-quality-services/data-matching.md)  
  
  
