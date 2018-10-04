---
title: 데이터 마이닝 알고리즘 (SQL Server 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation
- data mining algorithms
- clustering [data mining]
- linear regression
- association [data mining]
- neural networks
- logistic regression
- regression
- sequence analysis
- decision tree [data mining]
- Naive Bayes
- time series [data mining]
ms.assetid: 3a1a62e4-9fb5-4cdb-a6c6-1b8b30d417ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b1feb34dca2fba1bad8829edff24ef1ce54e1fe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161563"
---
# <a name="data-mining-algorithms-sql-server-data-mining-add-ins"></a>데이터 마이닝 알고리즘(SQL Server 데이터 마이닝 추가 기능)
  Office용 데이터 마이닝 추가 기능은 다음과 같은 데이터 마이닝 알고리즘을 사용하여 분석 모델을 만드는 작업을 지원합니다. 모든 알고리즘은 잘 알려진 시스템 학습 방법을 기반으로 하며 Microsoft Research에서 구현되었습니다.  
  
## <a name="algorithms"></a>알고리즘  
  
|시스템 학습 방법|작동 방법|  
|-----------------------------|------------------|  
|Microsoft 연결 규칙 알고리즘|함께 구입하는 제품이나 함께 발생하는 이벤트를 발견하고 모델을 사용하여 권장 항목을 만듭니다.<br /><br /> [http://msdn.microsoft.com/library/ms174916.aspx](http://msdn.microsoft.com/library/ms174916.aspx)|  
|Microsoft 클러스터링 알고리즘|시장 세그먼트를 정의하거나, 관련 고객을 자동으로 함께 그룹화하거나, 이후 마이닝에서 사용할 관계를 데이터에서 찾습니다.<br /><br /> [http://msdn.microsoft.com/library/ms174879.aspx](http://msdn.microsoft.com/library/ms174879.aspx)|  
|Microsoft 의사 결정 트리 알고리즘|다양한 데이터 요소 간의 이전에 알려지지 않은 관계를 식별하여 결정에 더 많은 정보를 제공하거나, 특정 결과로 이끄는 요소를 찾습니다.<br /><br /> [http://msdn.microsoft.com/library/ms174923.aspx](http://msdn.microsoft.com/library/ms174923.aspx)|  
|Microsoft 선형 회귀 알고리즘|숫자 결과에 영향을 주는 요소를 설명하는 수식을 찾습니다.<br /><br /> [http://msdn.microsoft.com/library/ms174824.aspx](http://msdn.microsoft.com/library/ms174824.aspx)|  
|Microsoft 로지스틱 회귀 알고리즘|이진 결과에 영향을 주는 요소를 식별하고 이러한 요소를 사용하여 결과에 영향을 주는 방법을 파악합니다.<br /><br /> [http://msdn.microsoft.com/library/ms174828.aspx](http://msdn.microsoft.com/library/ms174828.aspx)|  
|Microsoft Naïve Bayes 알고리즘|데이터에서 관계를 탐색하고 결과와 가장 밀접히 연관된 관계를 찾습니다.<br /><br /> [http://msdn.microsoft.com/en-us/library/ms174806.aspx](http://msdn.microsoft.com/library/ms174806.aspx)|  
|Microsoft 신경망 알고리즘|여러 입력과 여러 출력 간의 숨겨진 관계를 찾습니다. 탐색이나 예측에 사용합니다.<br /><br /> [http://msdn.microsoft.com/library/ms174941.aspx](http://msdn.microsoft.com/library/ms174941.aspx)|  
|Microsoft 시계열 알고리즘|기록 데이터를 사용하여 미래 가치를 예측합니다.<br /><br /> [http://msdn.microsoft.com/library/ms174923.aspx](http://msdn.microsoft.com/library/ms174923.aspx)|  
  
## <a name="advanced-options"></a>고급 옵션  
 Excel용 데이터 마이닝 클라이언트를 사용할 때는 사용자 고유의 데이터 마이닝 구조 및 모델을 만들거나 알고리즘의 매개 변수를 세밀하게 조정하는 옵션이 제공됩니다.  
  
 [알고리즘 매개 변수 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md)  
  
 이러한 고급 옵션을 사용하여 모델을 사용자 지정하는 방법은 다음 두 가지입니다.  
  
-   **데이터 마이닝 쿼리** 마법사를 사용하여 모델을 만듭니다.  
  
-   **데이터 마이닝 클라이언트**에서 마법사를 시작한 후 **매개 변수**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](query-sql-server-data-mining-add-ins.md)   
 [고급 모델링 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
  
  
