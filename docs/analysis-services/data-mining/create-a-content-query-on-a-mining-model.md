---
title: "마이닝 모델에 내용 쿼리 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: content queries [DMX]
ms.assetid: a0ce837a-89ed-46cf-9ce1-801ccb75fa04
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4cff8211d13fe5ddf5fd1128f0fd53a0ab013ae1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-content-query-on-a-mining-model"></a>마이닝 모델에 내용 쿼리 만들기
  AMO 또는 XML/A를 사용하여 프로그래밍 방식으로 마이닝 모델 콘텐츠를 쿼리할 수 있지만 DMX를 사용하여 쿼리를 만드는 편이 더 쉽습니다. 또한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 제공하는 DMV를 사용해 쿼리를 작성하는 방식으로 데이터 마이닝 스키마 행 집합에 대한 쿼리를 만들 수 있습니다.  
  
 다음 절차에서는 DMX를 사용하여 마이닝 모델에 대한 쿼리를 만드는 방법과 데이터 마이닝 스키마 행 집합을 쿼리하는 방법을 보여 줍니다.  
  
 XML/A를 사용하여 비슷한 쿼리를 만드는 방법에 대한 예는 [XMLA를 사용하여 데이터 마이닝 쿼리 만들기](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)를 참조하세요.  
  
## <a name="querying-data-mining-model-content-by-using-dmx"></a>DMX를 사용하여 데이터 마이닝 모델 내용 쿼리  
  
#### <a name="to-create-a-dmx-model-content-query"></a>DMX 모델 내용 쿼리를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **템플릿 탐색기**를 클릭합니다.  
  
2.  **템플릿 탐색기** 창에서 큐브 아이콘을 클릭하여 목록을 변경하고 Analysis Services 템플릿을 표시합니다.  
  
3.  템플릿 범주 목록에서 **DMX**, **모델 콘텐츠**를 차례로 확장하고 **내용 쿼리**를 두 번 클릭합니다.  
  
4.  **Analysis Services에 연결** 대화 상자에서 쿼리할 마이닝 모델이 포함된 인스턴스를 선택하고 **연결**을 클릭합니다.  
  
     적절한 코드 편집기에서 **내용 쿼리** 템플릿이 열립니다. 메타데이터 창에는 현재 데이터베이스에서 사용할 수 있는 모델의 목록이 표시됩니다. 데이터베이스를 변경하려면 **사용 가능한 데이터베이스** 목록에서 다른 데이터베이스를 선택합니다.  
  
5.  줄에서는 마이닝 모델의 이름을 입력 `FROM` [*\<마이닝 모델, 이름, MyModel >*]`.CONTENT`합니다. 마이닝 모델 이름에 공백이 포함된 경우 이름을 대괄호로 묶어야 합니다.  
  
     이름을 입력하기가 불편하면 **개체 탐색기** 에서 마이닝 모델을 선택하고 템플릿에 끌어다 놓으면 됩니다.  
  
6.  줄에 `SELECT`  *\<select 목록, expr list \* >* , 마이닝 모델 콘텐츠 스키마 행 집합의 열 이름을 입력 합니다.  
  
     마이닝 모델 내용 쿼리에서 반환할 수 있는 열의 목록을 보려면 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)에서 제공하는 DMV를 사용해 쿼리를 작성하는 방식으로 데이터 마이닝 스키마 행 집합에 대한 쿼리를 만들 수 있습니다.  
  
7.  필요에 따라 템플릿의 WHERE 절에 조건을 입력하여 특정 노드 또는 값으로 반환되는 행을 제한할 수 있습니다.  
  
8.  **실행**을 클릭합니다.  
  
## <a name="querying-the-data-mining-schema-rowsets"></a>데이터 마이닝 스키마 행 집합 쿼리  
  
#### <a name="to-create-a-query-against-the-data-mining-schema-rowset"></a>데이터 마이닝 스키마 행 집합에 대한 쿼리를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **새 쿼리** 도구 모음에서 **Analysis Services DMX 쿼리**또는 **Analysis Services MDX 쿼리**를 클릭합니다.  
  
2.  **Analysis Services에 연결** 대화 상자에서 쿼리할 개체가 포함된 인스턴스를 선택하고 **연결**을 클릭합니다.  
  
     적절한 코드 편집기에서 **내용 쿼리** 템플릿이 열립니다. 메타데이터 창에는 현재 데이터베이스에서 사용할 수 있는 개체의 목록이 표시됩니다. 데이터베이스를 변경하려면 **사용 가능한 데이터베이스** 목록에서 다른 데이터베이스를 선택합니다.  
  
3.  쿼리 편집기에서 다음을 입력합니다.  
  
     `SELECT *`  
  
     `FROM $system.DMSCHEMA_MINING_MODEL_CONTENT`  
  
     `WHERE MODEL_NAME = '<model name>'`  
  
4.  **실행**을 클릭합니다.  
  
     결과 창에 모델의 콘텐츠가 표시됩니다.  
  
    > [!NOTE]  
    >  현재 인스턴스에서 쿼리할 수 있는 모든 스키마 행 집합의 목록을 보려면 `SELECT * FROM $system.`DISCOVER_SCHEMA_ROWSETS 쿼리를 사용합니다. 또는 데이터 마이닝과 관련된 스키마 행 집합의 목록은 [Data Mining Schema Rowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [데이터 마이닝 스키마 행 집합](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
