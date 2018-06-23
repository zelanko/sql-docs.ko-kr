---
title: 데이터 품질 일치 열(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 79af46616a685d8e52086c3621a963c350db7abf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187021"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>데이터 품질 일치 열(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 데이터를 일치시킨 후 리본의 **데이터 품질** 그룹에서 **자세한 정보 표시** 를 클릭하여 일치하는 자세한 정보를 제공하는 열을 표시할 수 있습니다.  
  
 다음 표에는 데이터 일치를 수행할 때 표시되는 열이 나와 있습니다.  
  
|속성|Description|  
|----------|-----------------|  
|**CLUSTER_ID**|비슷한 레코드를 그룹화하는 데 사용되는 고유 식별자입니다. 비슷한 행은 모두 동일한 **CLUSTER_ID**를 가집니다. 행에 대해 **CLUSTER_ID** 가 표시되지 않으면 비슷한 레코드를 찾지 못한 것입니다.|  
|**RECORD_ID**|레코드를 식별하는 데 사용되는 고유 식별자입니다. MDS 저장소에 저장된 코드 값과 마찬가지로 레코드를 식별하는 데 사용되는 값입니다. 이 식별자는 일치 작업이 수행될 때마다 자동으로 생성됩니다.|  
|**PIVOT_MARK**|다른 레코드를 비교할 때 기준으로 사용되는 임의의 레코드이며 점수 값을 가지지 않습니다.|  
|**SCORE**|그룹의 레코드가 피벗 레코드와 어느 정도나 유사한지를 나타냅니다. 이 점수는 DQS에서 결정합니다. 레코드가 다른 레코드의 피벗 레코드이거나 일치 항목을 찾을 수 없으면 점수가 표시되지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 품질 일치 MDS에 추가 기능 Excel 용](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [유사한 데이터 일치&#40;Excel용 MDS 추가 기능&#41;](match-similar-data-mds-add-in-for-excel.md)   
 [데이터 일치](../../data-quality-services/data-matching.md)  
  
  