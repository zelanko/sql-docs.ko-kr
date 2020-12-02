---
description: 데이터 마이닝 모델 학습 대상
title: 데이터 마이닝 모델 학습 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingmodeltrainingdest.f1
- sql13.dts.designer.dmmtrainingtransformation.connection.f1
- sql13.dts.designer.dmmtrainingtransformation.columns.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b70fe92da0c7efb0e59dbc89505ad623cad64432
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127241"
---
# <a name="data-mining-model-training-destination"></a>데이터 마이닝 모델 학습 대상

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  데이터 마이닝 모델 학습 대상은 데이터 마이닝 모델 알고리즘을 통해 대상에서 수신하는 데이터를 전달함으로써 데이터 마이닝 모델을 학습합니다. 동일 데이터 마이닝 구조를 기반으로 모델을 작성한 경우에는 하나의 대상에서 여러 데이터 마이닝 모델의 성향을 습득할 수 있습니다. 자세한 내용은 [Mining Structure Columns](/analysis-services/data-mining/mining-structure-columns) 및 [Mining Model Columns](/analysis-services/data-mining/mining-model-columns)를 참조하세요.  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>데이터 마이닝 모델 학습 대상 구성  
 대상 구조의 사례 수준 열과 이 구조에서 작성된 모델의 내용 유형이 KEY TIME 또는 KEY SEQUENCE인 경우 입력 데이터는 해당 열에서 정렬되어야 합니다. 예를 들어 Microsoft Time Series 알고리즘을 사용하여 작성된 모델에서는 KEY TIME 내용 유형이 사용됩니다. 입력 데이터가 정렬되지 않은 경우 모델 처리가 실패할 수 있습니다. 데이터에 정렬이 필요한 경우 데이터 흐름의 초반에 정렬 변환을 사용하여 데이터를 정렬할 수 있습니다. 내용 유형이 KEY인 열에서는 이렇게 할 필요가 없습니다. 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](/analysis-services/data-mining/content-types-data-mining) 및 [정렬 변환](../../integration-services/data-flow/transformations/sort-transformation.md)을 참조하세요.  
  
> [!NOTE]  
>  데이터 마이닝 모델 학습 대상에 대한 입력은 정렬되어야 합니다. 데이터를 정렬하기 위해서는 데이터 마이닝 모델 학습 대상의 정렬 대상 업스트림을 데이터 흐름에 포함시킬 수 있습니다. 자세한 내용은 [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md)을 참조하세요.  
  
 이 대상에는 하나의 입력이 포함되며 출력은 포함되지 않습니다.  
  
 데이터 마이닝 모델 학습 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 대상이 학습하는 마이닝 구조와 마이닝 모델이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
-   [데이터 마이닝 모델 학습 대상 사용자 지정 속성](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="data-mining-model-training-editor-connection-tab"></a>데이터 마이닝 모델 학습 편집기(연결 탭)
  **데이터 마이닝 모델 학습 편집기** 대화 상자의 **연결** 페이지를 사용하여 성향을 습득할 마이닝 모델을 선택할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **Connection manager**  
 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 목록에서 선택하거나 아래에서 설명하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 새로 만들기 **단추를 사용하여 새** 연결을 만듭니다.  
  
 **새로 만들기**  
 **Analysis Services 연결 관리자 추가** 대화 상자를 사용하면 새 연결을 만들 수 있습니다.  
  
 **마이닝 구조**  
 사용 가능한 마이닝 구조 목록에서 선택하거나 **새로 만들기** 를 클릭하여 새 구조를 만듭니다.  
  
 **새로 만들기**  
 **데이터 마이닝 마법사** 를 사용하여 새 마이닝 구조와 마이닝 모델을 만듭니다.  
  
 **마이닝 모델**  
 선택한 마이닝 구조와 연관된 마이닝 모델 목록을 표시합니다.  
  
## <a name="data-mining-model-training-editor-columns-tab"></a>데이터 마이닝 모델 학습 편집기(열 탭)
  **데이터 마이닝 모델 학습 편집기** 대화 상자의 **열** 페이지를 사용하여 입력 열을 마이닝 구조의 열에 매핑할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다. 입력 열을 끌어 마이닝 구조 열에 매핑합니다.  
  
 **마이닝 구조 열**  
 마이닝 구조 열 목록을 볼 수 있습니다. 마이닝 구조 열을 끌어 사용 가능한 입력 열에 매핑합니다.  
  
 **입력 열**  
 위 테이블에서 선택한 입력 열을 표시합니다. 매핑 선택 항목을 변경하거나 제거하려면 **사용 가능한 입력 열** 목록을 사용합니다.  
  
 **마이닝 구조 열**  
 매핑 여부에 관계없이 사용 가능한 각 대상 열을 볼 수 있습니다.  
