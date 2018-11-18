---
title: 데이터 마이닝 쿼리 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
- sql13.dts.designer.dmquerytask.miningmodel.f1
- sql13.dts.designer.dmquerytask.query.f1
- sql13.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 184f3337f706d2a19210a8304d6b351b352ea309
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639900"
---
# <a name="data-mining-query-task"></a>Data Mining Query Task
  데이터 마이닝 쿼리 태스크는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 작성된 데이터 마이닝 모델을 기반으로 예측 쿼리를 실행합니다. 예측 쿼리는 마이닝 모델을 사용하여 새 데이터에 대한 예측을 만듭니다. 예를 들어 예측 쿼리는 여름 기간 동안 판매될 요트 수를 예측하거나 요트를 구매할 잠재 고객 목록을 생성할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 은 DDL(데이터 정의 언어) 문 실행과 분석 개체 처리 등의 기타 비즈니스 인텔리전스 작업을 수행하는 태스크를 제공합니다.  
  
 기타 비즈니스 인텔리전스 태스크에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services DDL 실행 태스크](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 처리 태스크](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>예측 쿼리  
 쿼리는 DMX(Data Mining Extensions) 문입니다. DMX 언어는 마이닝 모델 작업을 지원하는 SQL 언어의 확장입니다. DMX 언어를 사용하는 방법은 [DMX&#40;Data Mining Extensions&#41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)를 참조하세요.  
  
 이 태스크는 동일한 마이닝 구조를 사용하는 여러 개의 마이닝 모델을 쿼리할 수 있습니다. 마이닝 모델은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 데이터 마이닝 알고리즘 중 하나를 사용하여 작성합니다. 데이터 마이닝 쿼리 태스크가 참조하는 마이닝 구조에 다른 알고리즘을 사용하여 작성된 여러 개의 마이닝 모델이 포함될 수도 있습니다. 자세한 내용은 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md) 및 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요.  
  
 데이터 마이닝 쿼리 태스크가 실행하는 예측 쿼리는 단일 행이나 데이터 집합을 결과로 반환합니다. 단일 행을 반환하는 쿼리를 단일 쿼리라고 합니다. 예를 들어 여름 기간 동안 판매될 요트 수를 예측하는 쿼리는 한 개의 숫자를 반환합니다. 단일 행을 반환하는 예측 쿼리에 대한 자세한 내용은 [데이터 마이닝 쿼리 도구](../../analysis-services/data-mining/data-mining-query-tools.md)를 참조하세요.  
  
 쿼리 결과는 테이블에 저장됩니다. 지정한 이름의 테이블이 이미 있으면 데이터 마이닝 쿼리 태스크는 동일한 이름에 번호를 추가하여 새 테이블을 만들거나 테이블 내용을 덮어쓸 수 있습니다.  
  
 중첩이 포함된 결과는 저장되기 전에 결합됩니다. 결과를 결합하면 중첩 결과 집합이 테이블로 바뀝니다. 예를 들어 **Customer** 열과 중첩된 **Product** 열이 포함된 중첩 결과를 결합하면 **Customer** 열에 행이 추가되어 각 고객의 제품 데이터가 포함된 테이블이 생성됩니다. 예를 들어 3가지 제품을 가진 고객은 행이 3개인 테이블이 되며 각 행에는 해당 고객이 반복되고 서로 다른 제품이 포함됩니다. FLATTENED 키워드를 생략하면 테이블에 **Customer** 열만 포함되고 고객당 하나의 행이 있습니다. 자세한 내용은 [SELECT&#40;DMX&#41;](../../dmx/select-dmx.md)를 참조하세요.  
  
## <a name="configuration-of-the-data-mining-query-task"></a>데이터 마이닝 쿼리 태스크 구성  
 데이터 마이닝 쿼리 태스크에는 두 개의 연결이 필요합니다. 첫 번째 연결은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자입니다. 두 번째 연결은 태스크에서 데이터를 쓰는 테이블이 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 OLE DB 연결 관리자입니다. 자세한 내용은 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md) 및 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  데이터 마이닝 쿼리 편집기에는 식 페이지가 없습니다. 대신 **속성** 창을 사용하여 데이터 마이닝 쿼리 태스크의 속성 식을 만들고 관리하는 도구에 액세스할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>데이터 마이닝 쿼리 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
## <a name="data-mining-query-task-editor-mining-model-tab"></a>데이터 마이닝 쿼리 태스크 편집기(마이닝 모델 탭)
  **데이터 마이닝 쿼리 태스크** 대화 상자의 **마이닝 모델** 탭을 사용하여 사용할 마이닝 구조와 마이닝 모델을 지정할 수 있습니다.  
  
 패키지에서 데이터 마이닝을 구현하는 방법에 대한 자세한 내용은 [데이터 마이닝 쿼리 태스크](../../integration-services/control-flow/data-mining-query-task.md) 및 [데이터 마이닝 솔루션](../../analysis-services/data-mining/data-mining-solutions.md)을 참조하세요.  
  
### <a name="general-options"></a>일반 옵션  
 **이름**  
 데이터 마이닝 쿼리 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 데이터 마이닝 쿼리 태스크에 대한 설명을 입력합니다.  
  
### <a name="mining-model-tab-options"></a>마이닝 모델 탭 옵션  
 **대량 삽입 태스크 편집기**  
 목록에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:**  [Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **새로 만들기**  
 새로운 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 만듭니다.  
  
 **관련 항목:** [Analysis Services 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **마이닝 구조**  
 목록에서 마이닝 구조를 선택합니다.  
  
 **마이닝 모델**  
 선택한 마이닝 구조를 기반으로 하는 마이닝 모델을 선택합니다.  

## <a name="data-mining-query-task-editor-query-tab"></a>데이터 마이닝 쿼리 태스크 편집기(쿼리 탭)
  **데이터 마이닝 쿼리 태스크** 대화 상자의 **쿼리** 탭을 사용하여 마이닝 모델을 기반으로 하는 예측 쿼리를 만들 수 있습니다. 또한 이 대화 상자에서 매개 변수 및 결과 집합을 변수에 바인딩할 수 있습니다.  
  
 패키지에서 데이터 마이닝을 구현하는 방법에 대한 자세한 내용은 [데이터 마이닝 쿼리 태스크](../../integration-services/control-flow/data-mining-query-task.md) 및 [데이터 마이닝 솔루션](../../analysis-services/data-mining/data-mining-solutions.md)을 참조하세요.  
  
### <a name="general-options"></a>일반 옵션  
 **이름**  
 데이터 마이닝 쿼리 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 데이터 마이닝 쿼리 태스크에 대한 설명을 입력합니다.  
  
### <a name="build-query-tab-options"></a>쿼리 작성 탭 옵션  
 **데이터 마이닝 쿼리**  
 데이터 마이닝 쿼리를 입력합니다.  
  
 **관련 항목:** [DMX&#40;Data Mining Extensions&#41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)  
  
 **새 쿼리 작성**  
 그래픽 도구를 사용하여 데이터 마이닝 쿼리를 만듭니다.  
  
 **관련 항목:** [Data Mining Query](../../integration-services/control-flow/data-mining-query.md)  
  
### <a name="parameter-mapping-tab-options"></a>매개 변수 매핑 탭 옵션  
 **매개 변수 이름**  
 필요에 따라 매개 변수 이름을 업데이트합니다. **변수 이름** 목록에서 변수를 선택하여 매개 변수를 변수에 매핑합니다.  
  
 **변수 이름**  
 목록에서 매개 변수에 매핑할 변수를 선택합니다.  
  
 **추가**  
 목록에 매개 변수를 추가합니다.  
  
 **제거**  
 매개 변수를 선택한 다음 **제거**를 클릭합니다.  
  
### <a name="result-set-tab-options"></a>결과 집합 탭 옵션  
 **결과 이름**  
 필요에 따라 결과 집합 이름을 업데이트합니다. **변수 이름** 목록에서 변수를 선택하여 결과를 변수에 매핑합니다.  
  
 **추가**를 클릭하여 결과를 추가한 다음 결과에 사용할 고유 이름을 제공합니다.  
  
 **변수 이름**  
 목록에서 결과 집합에 매핑할 변수를 선택합니다.  
  
 **결과 유형**  
 단일 행을 반환할지, 아니면 전체 결과 집합을 반환할지 여부를 나타냅니다.  
  
 **추가**  
 목록에 결과 집합을 추가합니다.  
  
 **제거**  
 결과를 선택한 다음 **제거**를 클릭합니다.  
## <a name="data-mining-query-task-editor-output-tab"></a>데이터 마이닝 쿼리 태스크 편집기(출력 탭)
  **데이터 마이닝 쿼리 태스크 편집기** 대화 상자의 **출력** 탭을 사용하여 예측 쿼리의 대상을 지정할 수 있습니다.  
  
 패키지에서 데이터 마이닝을 구현하는 방법에 대한 자세한 내용은 [데이터 마이닝 쿼리 태스크](../../integration-services/control-flow/data-mining-query-task.md) 및 [데이터 마이닝 솔루션](../../analysis-services/data-mining/data-mining-solutions.md)을 참조하세요.  
  
### <a name="general-options"></a>일반 옵션  
 **이름**  
 데이터 마이닝 쿼리 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 데이터 마이닝 쿼리 태스크에 대한 설명을 입력합니다.  
  
### <a name="output-tab-options"></a>출력 탭 옵션  
 **대량 삽입 태스크 편집기**  
 목록에서 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다.  
  
 **새로 만들기**  
 새 연결 관리자를 만듭니다. ADO.NET 및 OLE DB 연결 관리자 유형만 사용할 수 있습니다.  
  
 **출력 테이블**  
 예측 쿼리가 결과를 작성할 테이블을 지정합니다.  
  
 **출력 테이블을 삭제하고 다시 만들기**  
 테이블을 삭제한 다음 다시 만들어 예측 쿼리가 대상 테이블의 내용을 덮어쓸지 여부를 나타냅니다.  
  
