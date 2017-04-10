---
title: "데이터 정의 쿼리(데이터 마이닝) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49e02de1-4ffa-401c-8eee-471a9c25b86a
caps.latest.revision: 12
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 12
---
# 데이터 정의 쿼리(데이터 마이닝)
  데이터 마이닝의 *데이터 정의 쿼리* 범주는 다음을 수행하는 DMX 문이나 XMLA 명령을 의미합니다.  
  
-   모델과 같은 데이터 마이닝 개체를 만들거나 변경하거나 조작합니다.  
  
-   학습이나 예측에 사용할 데이터의 원본을 정의합니다.  
  
-   마이닝 모델과 마이닝 구조를 내보내거나 가져옵니다.  
  
 [데이터 정의 쿼리 만들기](#bkmk_Create)  
  
-   [SQL Server Data Tools의 데이터 정의 쿼리](#bkmk_ssdt)  
  
-   [SQL Server Management Studio의 데이터 정의 쿼리](#bkmk_SSMS)  
  
 [데이터 정의 문 스크립팅](#bkmk_Scripts)  
  
 [데이터 정의 문 스크립팅](#bkmk_Export)  
  
##  <a name="bkmk_Create"></a> 데이터 정의 쿼리 만들기  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 예측 쿼리 작성기를 사용하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 DMX 쿼리 창을 사용하여 데이터 정의 쿼리(문)를 만들 수 있습니다. DMX의 데이터 정의 문은 Analysis Services DDL(데이터 정의 언어)의 일부입니다.  
  
 특정 데이터 정의 문의 구문에 대한 자세한 내용은 [DMX&#40;Data Mining Extensions&#41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)를 참조하세요.  
  
###  <a name="bkmk_ssdt"></a> SQL Server Data Tools의 데이터 정의 쿼리  
 데이터 마이닝 마법사는 마이닝 모델과 마이닝 구조를 만들고 수정하며 학습과 예측 쿼리에서 사용되는 데이터 원본을 정의하기 위한 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 기본 도구입니다.  
  
 그러나 마법사에서 데이터 구조나 마이닝 모델을 만들기 위해 서버에 보낼 문을 알고 싶은 경우 SQL Server Profiler를 사용하여 데이터 정의 문을 캡처할 수 있습니다. 자세한 내용은 [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)을(를) 참조하세요.  
  
 학습이나 예측에 사용되는 데이터 원본을 정의하는 데 사용되는 문을 보려면 예측 쿼리 작성기에서 **SQL 보기** 를 사용합니다. 경우에 따라 올바른 구문을 설정하기 위해 예측 쿼리 작성기를 사용하여 모델을 학습하고 테스트하기 위한 기본 쿼리를 작성하는 것이 유용할 수 있습니다. 그런 다음 **SQL보기** 로 전환하고 수동으로 쿼리를 편집할 수 있습니다. 자세한 내용은 [Manually Edit a Prediction Query](../../analysis-services/data-mining/manually-edit-a-prediction-query.md)을(를) 참조하세요.  
  
###  <a name="bkmk_SSMS"></a> SQL Server Management Studio의 데이터 정의 쿼리  
 데이터 마이닝 개체의 경우 데이터 정의 쿼리를 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   [CREATE MINING MODEL&#40;DMX&#41;](../../dmx/create-mining-model-dmx.md)을 사용하여 클러스터링 모델이나 의사 결정 트리 모델과 같은 특정 유형의 모델을 만듭니다.  
  
-   [ALTER MINING STRUCTURE&#40;DMX&#41;](../../dmx/alter-mining-structure-dmx.md)를 사용하여 모델을 추가하거나 열을 변경함으로써 기존 마이닝 구조를 변경합니다. DMX를 사용하여 마이닝 모델을 변경할 수 없습니다. 기존 구조에만 새 모델을 추가할 수 있습니다.  
  
-   [SELECT INTO&#40;DMX&#41;](../../dmx/select-into-dmx.md)를 사용하여 마이닝 모델의 복사본을 만든 다음 변경합니다.  
  
-   OPENROWSET와 같은 데이터 원본 쿼리와 함께 [INSERT INTO&#40;DMX&#41;](../../dmx/insert-into-dmx.md)를 사용하여 모델 학습에 사용되는 데이터 집합을 정의합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에는 데이터 정의 쿼리를 만드는 데 도움이 되는 쿼리 템플릿이 있습니다. 자세한 내용은 [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)을 참조하세요.  
  
 일반적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 대해 제공되는 템플릿에는 일반 구문 정의만 포함됩니다. 일반 구문 정의는 **쿼리** 창에 입력하거나 매개 변수를 입력하기 위해 제공되는 대화 상자를 사용하여 사용자 지정해야 합니다.  
  
 인터페이스를 사용하여 매개 변수를 입력하는 방법의 예는 [템플릿에서 단일 예측 쿼리 작성](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)을 참조하세요.  
  
###  <a name="bkmk_Scripts"></a> 데이터 정의 문 스크립팅  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 데이터 마이닝 개체를 만들거나 변경하거나 데이터 원본을 정의하는 데 사용할 수 있는 여러 스크립트 언어와 프로그래밍 언어를 제공합니다.  DMX가 데이터 마이닝 태스크를 촉진하도록 설계되었지만 XMLA 및 AMO를 사용하여 스크립트나 사용자 지정 코드에서 개체를 조작할 수도 있습니다.  
  
 Excel용 데이터 마이닝 추가 기능도 많은 쿼리 템플릿을 포함하며 복잡한 DMX 문을 작성하는 데 도움이 되는 **고급 쿼리 편집기**를 제공합니다. 대화식으로 쿼리를 작성한 다음 SQL 보기로 전환하여 DMX 문을 캡처할 수 있습니다.  
  
##  <a name="bkmk_Export"></a> 모델 내보내기 및 가져오기  
 DMX에서 데이터 정의 문을 사용하여 모델의 정의와 모델에 필요한 구조 및 데이터 원본을 내보낸 다음 해당 정의를 다른 서버로 가져올 수 있습니다. 내보내기 및 가져오기 사용은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스 간에 데이터 마이닝 모델과 마이닝 구조를 이동하는 가장 빠르고 쉬운 방법입니다. 자세한 내용은 [데이터 마이닝 솔루션 및 개체 관리](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)를 참조하세요.  
  
> [!WARNING]  
>  모델이 큐브 데이터 원본의 데이터를 기반으로 하는 경우 DMX를 사용하여 모델을 내보낼 수 없으며 대신 백업과 복원을 사용해야 합니다.  
  
##  <a name="bkmk_Tasks"></a> 관련 작업  
 다음 표에서는 데이터 정의 쿼리와 관련된 태스크의 링크를 제공합니다.  
  
|||  
|-|-|  
|DMX 쿼리에 대한 템플릿으로 작업합니다.|[SQL Server Management Studio에서 Analysis Services 템플릿 사용](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|예측 쿼리 작성기를 사용하여 모든 종류의 쿼리를 디자인합니다.|[예측 쿼리 작성기를 사용하여 예측 쿼리 만들기](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)|  
|SQL Server Profiler를 사용하여 쿼리 정의를 캡처하고 추적을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 모니터링합니다.|[SQL Server Profiler를 사용하여 Analysis Services 모니터링](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 제공되는 스크립트 언어와 프로그래밍 언어에 대해 자세히 알아봅니다.|[XMLA&#40;XML for Analysis&#41; 참조](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)<br /><br /> [AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 관리하는 방법을 알아봅니다.|[데이터 마이닝 개체 내보내기 및 가져오기](../../analysis-services/data-mining/export-and-import-data-mining-objects.md)<br /><br /> [EXPORT&#40;DMX&#41;](../../dmx/export-dmx.md)<br /><br /> [IMPORT&#40;DMX&#41;](../../dmx/import-dmx.md)|  
|외부 데이터를 쿼리하기 위한 OPENROWSET 및 다른 방법에 대해 자세히 알아봅니다.|[&#60;원본 데이터 쿼리&#62;](../Topic/%3Csource%20data%20query%3E.md).|  
  
## 관련 항목:  
 [데이터 마이닝 마법사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
  