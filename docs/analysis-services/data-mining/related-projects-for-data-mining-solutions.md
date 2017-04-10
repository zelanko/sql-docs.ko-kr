---
title: "데이터 마이닝 솔루션 관련 프로젝트 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc26489a-4c27-4b89-8215-6d245427c350
caps.latest.revision: 12
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 12
---
# 데이터 마이닝 솔루션 관련 프로젝트
  데이터 마이닝 솔루션에 필요한 최소 사항은 데이터 원본, 데이터 원본 뷰, 마이닝 구조 및 마이닝 모델을 정의하는 데이터 마이닝 프로젝트입니다. 하지만 일상적인 의사 결정 과정에서 데이터 마이닝 모델을 사용하는 경우 데이터 마이닝이 예측 분석 솔루션의 다른 부분과 통합되어야 하는데 여기에는 다음과 같은 프로세스와 구성 요소가 포함될 수 있습니다.  
  
-   데이터 및 변수 준비 및 선택. 데이터 정리, 여러 데이터 원본의 통합 및 메타데이터 관리, 데이터를 데이터 웨어하우스로 변환, 병합 및 업로드하는 작업이 여기에 포함됩니다.  
  
-   분석 보고, 예측 제시 및 데이터 마이닝 동작의 감사/추적  
  
-   다차원 모델 및 테이블 형식 모델을 사용하여 찾은 내용 살펴보기  
  
-   데이터 마이닝 솔루션을 조정하여 새 데이터 지원 또는 현재 분석을 기반으로 지원 인프라 변경  
  
 이 항목에서는 예측 분석 솔루션에 속해 있는 경우가 많은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 다른 기능에 대해 설명합니다. 이러한 기능은 데이터 준비 및 데이터 마이닝 프로세스를 지원하거나 분석 및 동작을 위한 도구를 제공하여 사용자를 지원합니다.  
  
 [Integration Services](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Data Quality Service](#bkmk_DQSetc)  
  
 [전체 텍스트 검색](#bkmk_FTSetc)  
  
 [의미 체계 인덱싱](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a> SQL Server Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 데이터 마이닝 프로젝트의 데이터 준비 및 학습 단계에 필요한 구성 요소 및 기능을 제공합니다. 스크립트와 같은 다른 도구를 사용하여 데이터 정리 및 준비 태스크를 수행할 수도 있지만 데이터 마이닝에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 사용하면 다음과 같은 이점이 있습니다.  
  
-   태스크를 반복, 자동화, 분기 및 확장이 가능한 워크플로의 일부로 표현할 수 있습니다.  
  
-   감사에 대한 지원이 확장되며 다양한 방법으로 오류를 캡처하고 이벤트를 기록할 수 있습니다.  
  
     데이터 계보를 캡처할 뿐만 아니라 데이터 변환 파이프라인을 통해 데이터에 대한 변경 내용을 모니터링할 수 있습니다.  
  
     SSIS 워크플로를 SQL Server의 데이터 변경 캡처 기능을 지원하는 기능과 통합할 수 있습니다.  
  
-   데이터 마이닝을 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 워크플로에 통합하여 들어오는 데이터를 여러 테이블에 논리적으로 분리할 수 있습니다. 예를 들어 예측 쿼리를 사용하여 새 고객을 메일 캠페인의 대상으로 사용하는 여러 그룹에 분리할 수 있습니다.  
  
 다음 목록에서는 데이터 마이닝 지원에 가장 많이 사용되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소에 대한 링크를 보여 줍니다.  
  
 **제어 흐름 구성 요소**  
  
-   [Analysis Services DDL 실행 태스크](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 처리 태스크](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [CDC 제어 태스크](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [데이터 정리](../../data-quality-services/data-cleansing.md)  
  
-   [데이터 마이닝 쿼리 태스크](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [데이터 프로파일링 태스크](../../integration-services/control-flow/data-profiling-task.md)  
  
 **데이터 흐름 구성 요소**  
  
-   [CDC 흐름 구성 요소](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [조건부 분할 변환](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [데이터 변환](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [데이터 마이닝 모델 학습 대상](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [데이터 마이닝 쿼리 변환](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [파생 열 변환](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [비율 샘플링 변환](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [용어 추출 변환](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [용어 조회 변환](../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a> SQL Server Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 대개 데이터 마이닝 솔루션의 중요 구성 요소로 간주되지 않지만 데이터 마이닝 솔루션의 표시에 유용한 다음 기능을 제공합니다.  
  
-   여러 원본의 데이터를 복잡한 보고서에 통합합니다. 분석가를 위해 모델 콘텐츠에 대한 쿼리를 만들고 최종 사용자를 위해 예측 및 추세를 보여 주는 보고서를 만듭니다.  
  
-   사용자가 기존 마이닝 모델을 직접 쿼리할 수 있도록 해 주는 보고서를 만듭니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]와 통합하여 OLAP 모델에서 만든 데이터 마이닝 차원 및 데이터 마이닝 큐브를 드릴스루하고 탐색할 수 있도록 지원합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 사용할 수 있는 매개 변수화 및 서식 지정 기능을 제공합니다.  
  
 DMX 쿼리가 데이터 원본인 경우 Reporting Services를 사용하는 방법은 다음 링크를 참조하세요.  
  
 [데이터 마이닝 모델에서 데이터 검색&#40;DMX&#41;&#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Analysis Services DMX 쿼리 디자이너 사용자 인터페이스](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [DMX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 DMX를 데이터 원본으로 사용할 필요는 없습니다. 데이터 마이닝용 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소는 예측 쿼리의 결과를 관계형 데이터베이스에 저장할 수 있도록 지원합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 사용하여 모델을 업데이트하는 워크플로를 설정한 경우 예측 및 기타 데이터 마이닝 쿼리 결과를 SQL Server에 저장하면 보고를 위해 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 또는 DMX와 인터페이스하지 않는 다른 도구를 사용할 수 있습니다.  
  
 Reporting Services를 데이터 원본에 대한 프레젠테이션 계층으로 사용하는 방법에 대한 자세한 내용은 [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)을 참조하세요.  
  
##  <a name="bkmk_DQSetc"></a> Data Quality Services  
 DQS(Data Quality Services)는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 새로 도입되었습니다. 데이터 문제로 인해 데이터 마이닝을 수행할 수 없을 수도 있기 때문에 반복되는 분석을 수행하거나 데이터 원본이 복잡한 대규모 조직에서 작업하는 데이터 마이닝 담당자는 DQS를 사용하는 잘 계획된 데이터 프로젝트가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 다른 스크립트를 사용하는 데이터 임시 정리보다 데이터 마이닝 지원에 더 안정적인 솔루션이라는 것을 알게 될 것입니다.  
  
 데이터 마이닝 솔루션에서 데이터 준비 및 데이터 무결성을 위해 다음과 같은 DQS 기능을 고려해야 합니다.  
  
 **원본 데이터를 분석하고 변경 내용을 제시하는 컴퓨터 기반 데이터 정리 프로세스**  
 DQS는 원본 데이터를 데이터 품질 공급자가 유지 관리하고 보증하는 클라우드 기반 참조 데이터와 비교할 수 있습니다.  
  
 DQS는 원시 원본 데이터를 분석하고 사용자 데이터에서 기술 자료를 만들 수도 있습니다. 처리된 데이터는 분류되어 추가로 처리할 수 있도록 사용자에게 표시됩니다. 정리 프로세스는 대화형이므로 데이터 관리자는 컴퓨터 기반 데이터 정리 프로세스가 제공하는 데이터를 승인, 거부 또는 수정할 수 있습니다.  
  
 이 프로세스를 통해 지속적으로 개선하거나 여러 데이터 개선 단계에서 다시 사용할 수 있는 기술 자료가 생성됩니다.  
  
 자세한 내용은 [Data Cleansing](../../data-quality-services/data-cleansing.md)을 참조하세요.  
  
 **원본 데이터를 분석하고 변경 내용을 제시하는 컴퓨터 기반 일치 과정**  
 데이터 중복을 막기 위해 데이터 원본의 추가 정리를 수행하여 정확하게 일치하는 항목 및 근사하게 일치하는 항목을 식별할 수 있습니다. 이 구성 요소를 통해 일치 규칙 및 이 규칙을 적용할 임계값을 지정할 수 있습니다.  
  
 일치하는 데이터를 찾음으로써 데이터 마이닝에 문제가 될 수 있는 중복 항목을 제거할 수 있습니다. 데이터 중복 제거는 자동으로 실행되지 않으므로 데이터 관리자 또는 IT 전문가는 기술 자료에 있는 정보와 해당 데이터에 대한 변경 내용을 모두 확인해야 합니다.  
  
 초기 DQS 프로젝트를 만든 후 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 사용하여 여러 태스크를 자동화할 수 있습니다.  
  
 자세한 내용은 [Data Matching](../../data-quality-services/data-matching.md)을 참조하세요.  
  
 데이터 품질 프로젝트에서 정리 및 일치 동작을 수행하는 동안 DQS에 의해 처리되는 데이터의 실시간 통계 및 정보를 얻을 수 있습니다. 데이터 프로파일링을 통해 데이터 정리 또는 일치 작업으로 데이터 품질이 개선된 정도를 평가하고 변경된 내용을 이해할 수 있습니다. 데이터 프로파일링 및 알림에 대한 자세한 내용은 [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md)을 참조하세요.  
  
 **세 가지 유형의 정보(바로 사용할 수 있게 준비된 정보, DQS 서버가 생성한 정보 및 사용자가 생성한 정보)를 나타내는 기술 자료입니다.**  
 기술 자료를 만들면 이 자료를 반복적으로 사용하여 다른 데이터를 정리 및 확인할 수 있습니다.  
  
 여러 원본에서 새 데이터를 기술 자료 데이터로 가져올 수 있습니다. 참조 공급자가 제공하는 알려진 정리된 데이터 또는 기술 자료의 기존 데이터와 일치하는 원시 데이터가 여기에 해당합니다.  
  
 데이터 품질 프로젝트의 정리 동작에 대한 자세한 내용은 데이터 정리(DQS)를 참조하십시오.  
  
 기술 자료의 정보를 다른 원본에 적용하여 다른 프로세스 내부에서 데이터 정리를 수행할 수도 있습니다. 이러한 데이터 정리를 통해 사용자 입력 오류, 전송 또는 저장 과정의 손상 또는 일치하지 않는 데이터 사전 정의를 식별할 수 있습니다.  
  
 자세한 내용은 [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하세요.  
  
##  <a name="bkmk_FTSetc"></a> 전체 텍스트 검색  
 SQL Server의 전체 텍스트 검색을 사용하면 응용 프로그램과 사용자가 SQL Server 테이블의 문자 기반 데이터에 대해 전체 텍스트 쿼리를 실행할 수 있습니다. 전체 텍스트 검색을 사용하면 여러 가지 형태의 단어 또는 구에 대한 언어별 규칙에 의해 개선된 텍스트 데이터에 대해 검색을 수행할 수 있습니다. 여러 용어 간 거리 등과 같은 검색 조건을 구성하고 가능성 순서로 반환된 결과를 제한하는 함수를 사용할 수도 있습니다.  
  
 전체 텍스트 쿼리는 SQL Server 엔진에서 제공하는 기능이기 때문에 매개 변수가 있는 쿼리를 만들고, 텍스트 데이터 원본에서 전체 텍스트 검색 기능을 사용하여 사용자 지정 데이터 집합 또는 용어 벡터를 생성하고, 데이터 마이닝에 이러한 원본을 사용할 수 있습니다.  
  
 전체 텍스트 쿼리가 전체 텍스트 인덱스와 상호 작용하는 방식은 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)를 참조하세요.  
  
 SQL Server의 전체 텍스트 검색 기능을 사용하면 모든 SQL Server 언어에 대해 제공되는 단어 분리기 및 형태소 분석기에 포함된 언어적 지능을 활용할 수 있습니다. 제공된 단어 분리기 및 형태소 분석기를 사용하면 단어가 각 언어에 적합한 문자를 사용하여 분리되고 분음 기호 또는 철자 변형 기준 동의어(예: 일본어의 다중 숫자 형식)가 무시되지 않도록 할 수 있습니다.  
  
 단어의 경계를 제어하는 언어적 지능 외에도 각 언어의 형태소 분석기는 해당 언어의 활용 및 철자 변형 규칙에 대한 정보를 기반으로 다양한 단어 변형을 단일 용어로 축소할 수 있습니다. 언어 분석에 대한 규칙은 언어마다 다르며 실제 언어 자료에 대한 광범위한 연구를 기반으로 개발됩니다.  
  
 자세한 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)를 참조하세요.  
  
 전체 텍스트 인덱싱 후 저장되는 단어의 버전은 압축된 형식의 토큰입니다. 전체 텍스트 인덱스에 대한 후속 쿼리가 수행됨에 따라 가능성 있는 모든 일치 항목을 찾을 수 있도록 해당 언어의 규칙에 따라 특정 단어의 여러 굴절형이 생성됩니다. 예를 들어 저장된 토큰은 "run"이더라도 쿼리 엔진은 "run"이라는 어원에서 파생된 형태학상의 변형인 "running", "ran" 및 "runner"도 검색합니다.  
  
 사용자 동의어 사전을 만들어 검색 결과를 향상시키거나 용어 범주화를 작성할 수도 있습니다. 전체 텍스트 데이터에 맞게 동의어 사전을 개발하면 해당 데이터에 대한 전체 텍스트 쿼리의 범위를 효과적으로 넓힐 수 있습니다. 자세한 내용은 [전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)를 참조하세요.  
  
 전체 텍스트 검색을 사용하는 데 필요한 요구 사항은 다음과 같습니다.  
  
-   데이터베이스 관리자가 해당 테이블에 대한 전체 텍스트 인덱스를 만들어야 합니다.  
  
-   테이블당 한 개의 전체 텍스트 인덱스만 허용합니다.  
  
-   인덱스에 포함되는 각 열은 고유 키를 가지고 있어야 합니다.  
  
-   데이터 형식이 char, varchar, nchar, nvarchar, text, ntext, image, xml, varbinary, varbinary(max) 등인 열에 대해서만 전체 텍스트 인덱싱이 지원됩니다. 열이 varbinary, varbinary(max), image 또는 xml이면 별도의 유형 열에 인덱싱 가능한 문서의 파일 확장명(.doc, .pdf, .xls 등)을 지정해야 합니다.  
  
##  <a name="bkmk_SemSearch"></a> 의미 체계 인덱싱  
 의미 체계 검색은 SQL Server의 기존 전체 텍스트 검색 기능을 기반으로 구축되지만 자동 키워드 추출 및 관련 문서 검색 등의 시나리오를 사용할 수 있도록 추가 기능 및 통계를 사용합니다. 예를 들어 의미 체계 검색을 사용하여 조직에 대한 기본 분류를 작성하거나 문서 모음을 분류할 수 있습니다. 추출된 용어 및 문서 유사성 점수 조합을 클러스터링 또는 의사 결정 트리 모델에서 사용할 수도 있습니다.  
  
 의미 체계 검색을 설정하고 데이터 열에 인덱스를 지정한 후 의미 체계 인덱싱에 기본적으로 제공되는 기능을 사용하여 다음과 같은 작업을 수행할 수 있습니다.  
  
-   단일 단어 키 구를 해당 점수와 함께 반환합니다.  
  
-   지정된 키 구가 포함된 문서를 반환합니다.  
  
-   유사성 점수와 해당 점수에 기여하는 용어를 반환합니다.  
  
 자세한 내용은 [의미 체계 검색을 사용하여 문서의 키 구 찾기](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) 및 [의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)를 참조하세요.  
  
 의미 체계 인덱싱을 지원하는 데이터베이스 개체에 대한 자세한 내용은 [테이블 및 열에 대한 의미 체계 검색 사용](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)을 참조하세요.  
  
 의미 체계 검색을 사용하는 데 필요한 요구 사항은 다음과 같습니다.  
  
-   전체 텍스트 검색도 사용하도록 설정되어야 합니다.  
  
-   의미 체계 검색 구성 요소를 설치하면 이름을 바꾸거나 변경하거나 교체할 수 없는 특수 시스템 데이터베이스도 생성됩니다.  
  
-   해당 서비스를 사용하여 인덱싱하는 문서는 SQL Server에서 테이블 및 인덱싱된 뷰와 같이 전체 텍스트 인덱싱이 지원되는 데이터베이스 개체에 저장되어야 합니다.  
  
-   일부 전체 텍스트 언어는 의미 체계 인덱싱을 지원하지 않습니다. 지원되는 언어 목록을 보려면 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)를 참조하세요.  
  
## 관련 항목:  
 [다차원 모델 솔루션&#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [테이블 형식 모델 솔루션&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)  
  
  