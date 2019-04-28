---
title: 데이터 마이닝 모델 학습 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingmodeltrainingdest.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9d00be2992f9ad661736f65e4d1146a34fe1fad0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827979"
---
# <a name="data-mining-model-training-destination"></a>데이터 마이닝 모델 학습 대상
  데이터 마이닝 모델 학습 대상은 데이터 마이닝 모델 알고리즘을 통해 대상에서 수신하는 데이터를 전달함으로써 데이터 마이닝 모델을 학습합니다. 동일 데이터 마이닝 구조를 기반으로 모델을 작성한 경우에는 하나의 대상에서 여러 데이터 마이닝 모델의 성향을 습득할 수 있습니다. 자세한 내용은 [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md) 및 [Mining Model Columns](../../analysis-services/data-mining/mining-model-columns.md)를 참조하세요.  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>데이터 마이닝 모델 학습 대상 구성  
 대상 구조의 사례 수준 열과 이 구조에서 작성된 모델의 내용 유형이 KEY TIME 또는 KEY SEQUENCE인 경우 입력 데이터는 해당 열에서 정렬되어야 합니다. 예를 들어 Microsoft 시계열 알고리즘을 사용하여 작성된 모델에서는 KEY TIME 내용 유형이 사용됩니다. 입력 데이터가 정렬되지 않은 경우 모델 처리가 실패할 수 있습니다. 데이터에 정렬이 필요한 경우 데이터 흐름의 초반에 정렬 변환을 사용하여 데이터를 정렬할 수 있습니다. 내용 유형이 KEY인 열에서는 이렇게 할 필요가 없습니다. 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md) 및 [정렬 변환](transformations/sort-transformation.md)을 참조하세요.  
  
> [!NOTE]  
>  데이터 마이닝 모델 학습 대상에 대한 입력은 정렬되어야 합니다. 데이터를 정렬하기 위해서는 데이터 마이닝 모델 학습 대상의 정렬 대상 업스트림을 데이터 흐름에 포함시킬 수 있습니다. 자세한 내용은 [Sort Transformation](transformations/sort-transformation.md)을 참조하세요.  
  
 이 대상에는 하나의 입력이 포함되며 출력은 포함되지 않습니다.  
  
 데이터 마이닝 모델 학습 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 학습 대상의 마이닝 구조와 마이닝 모델이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **데이터 마이닝 모델 학습 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [데이터 마이닝 모델 학습 편집기&#40;연결 탭&#41;](../data-mining-model-training-editor-connection-tab.md)  
  
-   [데이터 마이닝 모델 학습 편집기&#40;열 탭&#41;](../data-mining-model-training-editor-columns-tab.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../common-properties.md)  
  
-   [데이터 마이닝 모델 학습 대상 사용자 지정 속성](data-mining-model-training-destination-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
