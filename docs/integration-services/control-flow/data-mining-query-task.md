---
title: "데이터 마이닝 쿼리 태스크 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataminingquerytask.f1"
helpviewer_keywords: 
  - "예측 쿼리 [Integration Services]"
  - "데이터 마이닝 쿼리 태스크 [Integration Services]"
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
caps.latest.revision: 45
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# 데이터 마이닝 쿼리 태스크
  데이터 마이닝 쿼리 태스크는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 작성된 데이터 마이닝 모델을 기반으로 예측 쿼리를 실행합니다. 예측 쿼리는 마이닝 모델을 사용하여 새 데이터에 대한 예측을 만듭니다. 예를 들어 예측 쿼리는 여름 기간 동안 판매될 요트 수를 예측하거나 요트를 구매할 잠재 고객 목록을 생성할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 은 DDL(데이터 정의 언어) 문 실행과 분석 개체 처리 등의 기타 비즈니스 인텔리전스 작업을 수행하는 태스크를 제공합니다.  
  
 기타 비즈니스 인텔리전스 태스크에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services DDL 실행 태스크](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 처리 태스크](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## 예측 쿼리  
 쿼리는 DMX(Data Mining Extensions) 문입니다. DMX 언어는 마이닝 모델 작업을 지원하는 SQL 언어의 확장입니다. DMX 언어를 사용하는 방법은 [DMX&#40;Data Mining Extensions&#41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)를 참조하세요.  
  
 이 태스크는 동일한 마이닝 구조를 사용하는 여러 개의 마이닝 모델을 쿼리할 수 있습니다. 마이닝 모델은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 데이터 마이닝 알고리즘 중 하나를 사용하여 작성합니다. 데이터 마이닝 쿼리 태스크가 참조하는 마이닝 구조에 다른 알고리즘을 사용하여 작성된 여러 개의 마이닝 모델이 포함될 수도 있습니다. 자세한 내용은 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md) 및 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요.  
  
 데이터 마이닝 쿼리 태스크가 실행하는 예측 쿼리는 단일 행이나 데이터 집합을 결과로 반환합니다. 단일 행을 반환하는 쿼리를 단일 쿼리라고 합니다. 예를 들어 여름 기간 동안 판매될 요트 수를 예측하는 쿼리는 한 개의 숫자를 반환합니다. 단일 행을 반환하는 예측 쿼리에 대한 자세한 내용은 [데이터 마이닝 쿼리 도구](../../analysis-services/data-mining/data-mining-query-tools.md)를 참조하세요.  
  
 쿼리 결과는 테이블에 저장됩니다. 지정한 이름의 테이블이 이미 있으면 데이터 마이닝 쿼리 태스크는 동일한 이름에 번호를 추가하여 새 테이블을 만들거나 테이블 내용을 덮어쓸 수 있습니다.  
  
 중첩이 포함된 결과는 저장되기 전에 결합됩니다. 결과를 결합하면 중첩 결과 집합이 테이블로 바뀝니다. 예를 들어 **Customer** 열과 중첩된 **Product** 열이 포함된 중첩 결과를 결합하면 **Customer** 열에 행이 추가되어 각 고객의 제품 데이터가 포함된 테이블이 생성됩니다. 예를 들어 3가지 제품을 가진 고객은 행이 3개인 테이블이 되며 각 행에는 해당 고객이 반복되고 서로 다른 제품이 포함됩니다. FLATTENED 키워드를 생략하면 테이블에 **Customer** 열만 포함되고 고객당 하나의 행이 있습니다. 자세한 내용은 [SELECT&#40;DMX&#41;](../../dmx/select-dmx.md)를 참조하세요.  
  
## 데이터 마이닝 쿼리 태스크 구성  
 데이터 마이닝 쿼리 태스크에는 두 개의 연결이 필요합니다. 첫 번째 연결은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스 또는 마이닝 구조와 마이닝 모델이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자입니다. 두 번째 연결은 태스크에서 데이터를 쓰는 테이블이 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 OLE DB 연결 관리자입니다. 자세한 내용은 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md) 및 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [데이터 마이닝 쿼리 태스크 편집기&#40;마이닝 모델 탭&#41;](../../integration-services/control-flow/data-mining-query-task-editor-mining-model-tab.md)  
  
-   [데이터 마이닝 쿼리 태스크 편집기&#40;쿼리 탭&#41;](../../integration-services/control-flow/data-mining-query-task-editor-query-tab.md)  
  
-   [데이터 마이닝 쿼리 태스크 편집기&#40;출력 탭&#41;](../../integration-services/control-flow/data-mining-query-task-editor-output-tab.md)  
  
> [!NOTE]  
>  데이터 마이닝 쿼리 편집기에는 식 페이지가 없습니다. 대신 **속성** 창을 사용하여 데이터 마이닝 쿼리 태스크의 속성 식을 만들고 관리하는 도구에 액세스할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## 데이터 마이닝 쿼리 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
  