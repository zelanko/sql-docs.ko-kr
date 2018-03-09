---
title: "Integration Services 변환 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transformations [Integration Services], listed
- transformations [Integration Services], types
- transformations [Integration Services]
- data flow [Integration Services], transformations
- business intelligence transformations [Integration Services]
- join transformations
- split transformations [Integration Services]
- custom transformations [Integration Services]
- row transformations [Integration Services]
- rowset transformations [Integration Services]
ms.assetid: c70c4f6e-82dd-4948-b923-fd5193f67f7e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c2e4f97d129840e2c045fe942996a5918163c137
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-transformations"></a>Integration Services 변환
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 변환은 패키지의 데이터 흐름에서 데이터를 집계, 병합, 배포 및 수정하는 구성 요소입니다. 변환은 조회 작업을 수행하고 예제 데이터 집합을 생성할 수도 있습니다. 이 섹션에서는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에 포함되는 변환과 이러한 변환의 작동 방식에 대해 설명합니다.  
  
## <a name="business-intelligence-transformations"></a>비즈니스 인텔리전스 변환  
 다음 변환은 데이터 정리, 텍스트 마이닝 및 데이터 마이닝 예측 쿼리 실행과 같은 비즈니스 인텔리전스 작업을 수행합니다.  
  
|변환|Description|  
|--------------------|-----------------|  
|[느린 변경 차원 변환](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)|느린 변경 차원의 업데이트를 구성하는 변환입니다.|  
|[유사 항목 그룹화 변환](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)|열 데이터의 값을 표준화하는 변환입니다.|  
|[유사 항목 조회 변환](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)|유사 항목 일치를 사용하여 참조 테이블의 값을 조회하는 변환입니다.|  
|[용어 추출 변환](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)|텍스트에서 용어를 추출하는 변환입니다.|  
|[용어 조회 변환](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)|참조 테이블에서 용어를 조회하고 텍스트에서 추출된 용어의 개수를 세는 변환입니다.|  
|[데이터 마이닝 쿼리 변환](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|데이터 마이닝 예측 쿼리를 실행하는 변환입니다.|  
|[DQS 정리 변환](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)|데이터 원본에 대해 만든 규칙을 적용하여 연결된 데이터 원본에서 데이터를 수정하는 변환입니다.|  
  
## <a name="row-transformations"></a>행 변환  
 다음 변환은 열 값을 업데이트하고 새 열을 만듭니다. 변환은 변환 입력의 각 행에 적용됩니다.  
  
|변환|Description|  
|--------------------|-----------------|  
|[문자표 변환](../../../integration-services/data-flow/transformations/character-map-transformation.md)|문자 데이터에 문자열 함수를 적용하는 변환입니다.|  
|[열 복사 변환](../../../integration-services/data-flow/transformations/copy-column-transformation.md)|입력 열의 복사본을 변환 출력에 추가하는 변환입니다.|  
|[데이터 변환](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)|열의 데이터 형식을 다른 데이터 형식으로 변환하는 변환입니다.|  
|[파생 열 변환](../../../integration-services/data-flow/transformations/derived-column-transformation.md)|열에 식 결과를 채우는 변환입니다.|  
|[열 내보내기 변환](../../../integration-services/data-flow/transformations/export-column-transformation.md)|데이터 흐름의 데이터를 파일에 삽입하는 변환입니다.|  
|[열 가져오기 변환](../../../integration-services/data-flow/transformations/import-column-transformation.md)|파일에서 데이터를 읽고 이를 데이터 흐름에 추가하는 변환입니다.|  
|[스크립트 구성 요소](../../../integration-services/data-flow/transformations/script-component.md)|스크립트를 사용하여 데이터를 추출, 변환 또는 로드하는 변환입니다.|  
|[OLE DB 명령 변환](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)|데이터 흐름의 각 행에 대해 SQL 명령을 실행하는 변환입니다.|  
  
## <a name="rowset-transformations"></a>행 집합 변환  
 다음 변환은 새 행 집합을 만듭니다. 행 집합에는 집계 및 정렬 값, 예제 행 집합 또는 피벗된 행 집합과 피벗되지 않은 행 집합이 포함될 수 있습니다.  
  
|변환|Description|  
|--------------------|-----------------|  
|[집계 변환](../../../integration-services/data-flow/transformations/aggregate-transformation.md)|AVERAGE, SUM 및 COUNT와 같은 집계를 수행하는 변환입니다.|  
|[정렬 변환](../../../integration-services/data-flow/transformations/sort-transformation.md)|데이터를 정렬하는 변환입니다.|  
|[비율 샘플링 변환](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)|백분율을 사용하여 예제 크기를 지정하는 예제 데이터 집합을 만드는 변환입니다.|  
|[행 샘플링 변환](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)|예제에서 여러 행을 지정하여 예제 데이터 집합을 만드는 변환입니다.|  
|[피벗 변환](../../../integration-services/data-flow/transformations/pivot-transformation.md)|정규화된 테이블을 덜 정규화된 버전으로 만드는 변환입니다.|  
|[피벗 해제 변환](../../../integration-services/data-flow/transformations/unpivot-transformation.md)|정규화되지 않은 테이블을 보다 정규화된 버전으로 만드는 변환입니다.|  
  
## <a name="split-and-join-transformations"></a>분할 및 조인 변환  
 다음 변환은 행을 여러 출력에 배포하고, 변환 입력의 복사본을 만들고, 여러 입력을 하나의 출력으로 조인하고, 조회 작업을 수행합니다.  
  
|변환|Description|  
|--------------------|-----------------|  
|[조건부 분할 변환](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)|데이터 행을 여러 출력으로 라우팅하는 변환입니다.|  
|[멀티캐스트 변환](../../../integration-services/data-flow/transformations/multicast-transformation.md)|데이터 집합을 여러 출력에 배포하는 변환입니다.|  
|[UNION ALL 변환](../../../integration-services/data-flow/transformations/union-all-transformation.md)|여러 데이터 집합을 병합하는 변환입니다.|  
|[병합 변환](../../../integration-services/data-flow/transformations/merge-transformation.md)|두 개의 정렬된 데이터 집합을 병합하는 변환입니다.|  
|[병합 조인 변환](../../../integration-services/data-flow/transformations/merge-join-transformation.md)|FULL, LEFT 또는 INNER 조인을 사용하여 두 데이터 집합을 조인하는 변환입니다.|  
|[조회 변환](../../../integration-services/data-flow/transformations/lookup-transformation.md)|정확한 일치 항목을 사용하여 참조 테이블의 값을 조회하는 변환입니다.|  
|[캐시 변환](../../../integration-services/data-flow/transformations/cache-transform.md)|데이터 흐름에 있는 연결된 데이터 원본에서 캐시 파일에 데이터를 저장하는 캐시 연결 관리자에 데이터를 기록하는 변환입니다. 조회 변환은 캐시 파일의 데이터에 대한 조회를 수행합니다.|  
|[분산 데이터 배포자 변환](../../../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)|변환을 통해 들어오는 행의 버퍼를 여러 스레드의 출력에 균일하게 분산하여 다중 코어 및 다중 프로세서 서버에서 실행되는 SSIS 패키지의 성능을 향상시킵니다.|  
  
## <a name="auditing-transformations"></a>변환 감사  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에는 감사 정보를 추가하고 행 개수를 세기 위한 다음과 같은 변환이 포함됩니다.  
  
|변환|Description|  
|--------------------|-----------------|  
|[감사 변환](../../../integration-services/data-flow/transformations/audit-transformation.md)|환경 정보를 패키지의 데이터 흐름에서 사용할 수 있도록 만드는 변환입니다.|  
|[행 개수 변환](../../../integration-services/data-flow/transformations/row-count-transformation.md)|변환을 통과하는 행 개수를 세고 최종 개수를 변수에 저장하는 변환입니다.|  
  
## <a name="custom-transformations"></a>사용자 지정 변환  
 사용자 지정 변환을 작성할 수도 있습니다. 자세한 내용은 [동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) 및 [비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)을 참조하세요.  
  
  
