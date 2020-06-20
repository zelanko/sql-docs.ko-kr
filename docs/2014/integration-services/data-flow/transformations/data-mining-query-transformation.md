---
title: 데이터 마이닝 쿼리 변환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytrans.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 10a8c6495fc7d839132d102d9e696263a6f9df17
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939634"
---
# <a name="data-mining-query-transformation"></a>데이터 마이닝 쿼리 변환
  데이터 마이닝 쿼리 변환은 데이터 마이닝 모델과 비교해서 예측 쿼리를 수행합니다. 이 변환에는 DMX(Data Mining Extensions) 쿼리를 만들기 위한 쿼리 작성기가 포함되어 있습니다. 쿼리 작성기를 사용하면 DMX 언어를 사용하는 기존 마이닝 모델과 비교해서 변환 입력 데이터를 평가하는 사용자 지정 문을 만들 수 있습니다. 자세한 내용은 [DMX&#40;Data Mining Extensions&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)를 참조하세요.  
  
 모델이 동일한 데이터 마이닝 구조를 기반으로 하는 경우 하나의 변환에서 여러 개의 예측 쿼리를 실행할 수 있습니다. 자세한 내용은 [데이터 마이닝 쿼리 인터페이스](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)를 참조 하세요.  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>데이터 마이닝 쿼리 변환 구성  
 데이터 마이닝 쿼리 변환은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 마이닝 구조와 마이닝 모델이 포함된 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 인스턴스나 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 프로젝트에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../../connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **데이터 마이닝 쿼리 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [데이터 마이닝 쿼리 변환 편집기&#40;마이닝 모델 탭&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [데이터 마이닝 쿼리 변환 편집기&#40;마이닝 모델 탭&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
