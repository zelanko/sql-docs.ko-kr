---
title: "데이터 품질 일치 열 (MDS 추가 기능 Excel 용) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4ce8ddcdbf8c29663640025ad40b4e01e44d99c1
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>데이터 품질 일치 열(Excel용 MDS 추가 기능)
  에 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 데이터를 일치 시킨 후는 **데이터 품질** 그룹 리본에서 클릭할 수 있는 **자세한 정보 표시** 일치 하는 세부 정보를 제공 하는 열을 표시 합니다.  
  
 다음 표에는 데이터 일치를 수행할 때 표시되는 열이 나와 있습니다.  
  
|이름|Description|  
|----------|-----------------|  
|**CLUSTER_ID**|비슷한 레코드를 그룹화하는 데 사용되는 고유 식별자입니다. 비슷한 행은 모두 동일한 **CLUSTER_ID**를 가집니다. 행에 대해 **CLUSTER_ID** 가 표시되지 않으면 비슷한 레코드를 찾지 못한 것입니다.|  
|**RECORD_ID**|레코드를 식별하는 데 사용되는 고유 식별자입니다. MDS 저장소에 저장된 코드 값과 마찬가지로 레코드를 식별하는 데 사용되는 값입니다. 이 식별자는 일치 작업이 수행될 때마다 자동으로 생성됩니다.|  
|**PIVOT_MARK**|다른 레코드를 비교할 때 기준으로 사용되는 임의의 레코드이며 점수 값을 가지지 않습니다.|  
|**SCORE**|그룹의 레코드가 피벗 레코드와 어느 정도나 유사한지를 나타냅니다. 이 점수는 DQS에서 결정합니다. 레코드가 다른 레코드의 피벗 레코드이거나 일치 항목을 찾을 수 없으면 점수가 표시되지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 품질 일치 MDS에 추가 기능 Excel 용](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [유사한 데이터 &#40; 일치 MDS에 추가 기능 Excel &#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [데이터 일치](../../data-quality-services/data-matching.md)  
  
  
