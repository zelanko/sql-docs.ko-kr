---
title: 데이터 탐색 및 지우기 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94d1ea0bf396b8d839463fa648dffc3aacee9ab5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080473"
---
# <a name="exploring-and-cleaning-data"></a>데이터 탐색 및 지우기
  데이터 준비는 데이터 정리보다 훨씬 많이 수행됩니다. 데이터가 준비되는 방식은 결과가 결국 해석되는 방식에도 영향을 미칩니다. 데이터 준비는 다음과 같은 태스크로 이루어집니다.  
  
-   데이터 분포 탐색 및 확인  
  
-   잘못된 레코드 정리 및 데이터 마이닝 열 선택  
  
-   적절하게 Null 처리  
  
-   다양한 시간 단위를 기준으로 값 범주화 또는 값 집계  
  
-   결과의 사용 편의성을 높이기 위해 레이블 추가  
  
-   분석에 필요한 경우 데이터 형식 변환 또는 값 범주화  
  
 데이터 모델링을 처음 접하는 경우 관련된 항목을 읽어보는 것이 좋습니다 [검사 목록의 Preparation for Data Mining](checklist-of-preparation-for-data-mining.md)합니다.  
  
## <a name="data-preparation-tools"></a>데이터 준비 도구  
 Office용 데이터 마이닝 추가 기능에는 다음과 같은 데이터 정리 및 준비 도구가 포함됩니다.  
  
### <a name="explore-data"></a>데이터 탐색  
 사용 된 **데이터 탐색** 이러한 데이터 준비 작업에 대 한 마법사:  
  
-   분석하기 전에 데이터를 미리 보고 수정이 필요한 오류를 식별합니다.  
  
-   데이터의 균형과 필요한 정리 태스크를 이해하는 데 유용한 통계 정보를 수집합니다.  
  
-   분석에 유용한 열을 식별하고 데이터 모델링 단계를 계획합니다.  
  
 [데이터 탐색 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](explore-data-sql-server-data-mining-add-ins.md)합니다.  
  
### <a name="detect-and-handle-outliers"></a>이상값 검색 및 처리  
 합니다 **이상** 마법사에 데이터의 값 분포가 그래프로 표시 되며 극단적인 값을 제거할 수 있습니다. 사용 된 **이상** 다음 데이터 준비 작업에 대 한 도구:  
  
-   데이터의 패턴에 따라 개별 값을 신뢰할 수 있는지 확인합니다.  
  
-   비정상적인 값을 검토한 후 삭제 또는 교체합니다.  
  
-   모델을 특정 범위의 값으로 정의 예를 들어, 특정 저장소에 이상값이 있다는 것을 아는 경우 이 값을 제거하고 다른 저장소를 보다 잘 예측하는 모델을 가져올 수 있습니다.  
  
 [이상 값 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](outliers-sql-server-data-mining-add-ins.md)합니다.  
  
### <a name="relabel-and-bin-data"></a>데이터 레이블 재지정 및 범주화  
 합니다 **레이블 재지정** 마법사 데이터의 레이블을 변경할 수 없도록 값으로 데이터를 그룹화 합니다. 다음 데이터 준비 작업에 레이블 재지정 도구를 사용합니다.  
  
-   설문 조사 결과에 사용된 숫자 코드를 해당 숫자 코드가 의미하는 바에 대한 텍스트 설명으로 변경합니다.  
  
     예를 들어 성별 = 1과 같은 데이터 항목을 성별 = 여성으로 바꿀 수 있습니다.  
  
-   숫자 범위를 나타내는 그룹을 만들어 데이터를 범주화합니다.  
  
     숫자의 Income 열 레이블와 같은 대체 하려는 하는 예를 들어 **수입-보통** 하 고 **수입-높음**합니다.  
  
-   고유 값들을 범주별로 분류합니다.  
  
     예를 들어 개별 제품의 수가 너무 많아 구매 간 패턴을 검색하기 어려운 경우 더 광범위한 범주에 제품을 할당할 수 있습니다.  
  
 [레이블 재지정 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>데이터 지우기  
 데이터 정리는 다음과 같은 다양한 작업을 포함하며 대부분 추가 기능에서 지원합니다.  
  
-   Null 값을 식별하고 이러한 값을 실제 값으로 변경할지 또는 `Missing` 값으로 처리할지 여부를 결정합니다.  
  
-   누락된 값을 탐색하여 제거하거나 중간값, Null 또는 기타 값 등의 적절한 값으로 돌립니다.  
  
 [데이터 탐색 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [레이블 재지정 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [예제로 채우기](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>데이터 샘플링  
 데이터 샘플링 마법사에서 모델 학습 및 테스트에 사용되는 균형 잡힌 데이터 집합을 만드는 방법은 두 가지입니다.  
  
-   **무작위 샘플링 합니다.** 학습 또는 테스트에 사용하기 위해 큰 데이터 집합에서 대표성을 지닌 데이터 집합을 추출하려면 이 옵션을 사용합니다. 데이터 마이닝 추가 기능 사용 *층 별 샘플링* 에 샘플링 된 각 변수에 대해 균형 잡힌된 값 집합은 가져온 것인지 확인 합니다.  
  
-   **과다 샘플링 합니다.** 대상 결과에 사용하려는 것보다 데이터의 양이 적고 해당 데이터의 가중치를 높게 잡아야 하는 경우 이 옵션을 사용합니다. 예를 들어 부정 행위가 거의 발생하지 않을 수 있지만 부정 행위와 관련된 사례를 과다 샘플링하여 모델링에 충분한 데이터를 구할 수 있습니다.  
  
 [샘플 데이터 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](sample-data-sql-server-data-mining-add-ins.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)   
 [모델 유효성 검사 및 예측 용 모델 사용 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [마이닝 모델 배포 및 확장 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
