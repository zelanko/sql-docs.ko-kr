---
title: 데이터 마이닝 쿼리 태스크 및 방법 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], how-to topics
ms.assetid: 1bc2a775-6e62-4c66-a53c-201f2ea66295
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfa2d33d949aad49701e5294329349dc231965db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722856"
---
# <a name="data-mining-query-tasks-and-how-tos"></a>데이터 마이닝 쿼리 태스크 및 방법
  데이터 마이닝 모델을 사용하려는 경우 쿼리를 만드는 능력이 중요합니다. 이 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 제공된 도구를 사용하여 데이터 마이닝 모델에 대한 쿼리를 만드는 방법의 예를 보여 주는 링크를 제공합니다. 데이터 마이닝 쿼리가 무엇인지 또는 만들 수 있는 다양한 쿼리 유형에 대한 자세한 내용은 [데이터 마이닝 쿼리](data-mining-queries.md)를 참조하세요.  
  
## <a name="creating-queries-with-prediction-query-builder"></a>예측 쿼리 작성기를 사용하여 쿼리 만들기  
 예측 쿼리 작성기는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 데이터 마이닝 모델에 대해 그래픽을 통해 쿼리를 작성하는 방법으로 제공됩니다. 다음 항목에서는 모델을 선택하고 데이터 원본을 지정하고 예측을 사용자 지정하고 출력을 저장하는 방법에 대해 설명합니다.  
  
-   [예측 쿼리 작성기를 사용하여 예측 쿼리 만들기](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [데이터 마이닝 디자이너에서 단일 쿼리 작성](create-a-singleton-query-in-the-data-mining-designer.md)  
  
-   [예측 쿼리 작성기를 사용하여 예측 쿼리 만들기](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [예측 쿼리 결과 보기 및 저장](view-and-save-the-results-of-a-prediction-query.md)  
  
-   [예측 쿼리 수동 편집](manually-edit-a-prediction-query.md)  
  
-   [모델에 예측 함수 적용](apply-prediction-functions-to-a-model.md)  
  
-   [예측 쿼리에 대한 입력 데이터 선택 및 매핑](choose-and-map-input-data-for-a-prediction-query.md)  
  
## <a name="using-other-data-mining-query-tools"></a>기타 데이터 마이닝 쿼리 도구 사용  
 예측 쿼리 작성기를 사용하는 방법 외에도 DMX 또는 XMLA를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 직접 쿼리를 입력할 수도 있습니다. 프로그래밍 방식으로 예측 쿼리를 작성하고 작성한 쿼리를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에 보낼 수도 있습니다. 다음 항목에서는 예측 쿼리 작성기 외부에서 예측 쿼리를 만들고 사용하는 방법에 대한 자세한 내용을 제공합니다.  
  
 [템플릿에서 단일 예측 쿼리 작성](create-a-singleton-prediction-query-from-a-template.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 도구를 사용하여 예측 쿼리를 작성 및 실행하는 방법에 대해 설명합니다.  
  
 [템플릿에서 단일 예측 쿼리 작성](create-a-singleton-prediction-query-from-a-template.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 제공하는 템플릿을 사용하여 예측 쿼리에 매개 변수를 추가하는 방법을 설명합니다.  
  
 [데이터 마이닝 쿼리에 대한 제한 시간 값 변경](change-the-time-out-value-for-data-mining-queries.md)  
 서버에서 데이터 마이닝 쿼리와 관련된 동작을 제어하는 속성을 설정하는 방법에 대해 설명합니다.  
  
 [마이닝 모델에 내용 쿼리 만들기](create-a-content-query-on-a-mining-model.md)  
 데이터 마이닝 스키마 행 집합을 사용하여 마이닝 모델에 저장된 자세한 정보를 반환하는 쿼리를 만드는 방법에 대해 설명합니다.  
  
 [XMLA를 사용하여 데이터 마이닝 쿼리 만들기](create-a-data-mining-query-by-using-xmla.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 XMLA 템플릿을 사용하여 마이닝 모델 콘텐츠에 대한 쿼리를 만드는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 및 식 언어 참조&#40;Analysis Services&#41;](https://msdn.microsoft.com/library/gg492188(SQL.130).aspx)   
 [데이터 마이닝 저장 프로시저&#40;Analysis Services - 데이터 마이닝&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
