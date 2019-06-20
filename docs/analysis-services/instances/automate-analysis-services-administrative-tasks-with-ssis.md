---
title: Analysis Services Administrative Tasks with SSIS 자동화 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c750c0e8ee9f13c4b4751af872b02f4ed9ee419a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659596"
---
# <a name="automate-analysis-services-administrative-tasks-with-ssis"></a>SSIS를 사용하여 Analysis Services 관리 태스크 자동화
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] DDL 스크립트, 큐브 및 마이닝 모델 처리 태스크, 데이터 마이닝 쿼리 태스크의 실행을 자동화할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 순차 및 병렬 데이터 처리 작업을 구성하기 위해 연결할 수 있는 제어 흐름 및 유지 관리 태스크의 모음으로 생각할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 데이터 처리 태스크 중에 데이터 정리 작업을 수행하고 여러 다른 데이터 원본의 데이터를 결합하도록 디자인되었습니다. 큐브 및 마이닝 모델 작업 시에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 숫자가 아닌 데이터를 숫자 데이터로 변환할 수 있으며 데이터 값이 예상 범위 안에 포함되도록 만들어 팩트 테이블 및 차원을 채울 무결한 데이터를 만들 수 있습니다.  
  
## <a name="integration-services-tasks"></a>Integration Services 태스크  
 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 태스크 또는 작업에는 제어 흐름 요소 및 데이터 흐름 요소의 두 가지 주요 요소가 있습니다. 제어 흐름 요소는 선행 제약 조건을 적용하여 작업 처리 과정의 논리적 순서를 정의합니다. 데이터 흐름 요소는 구성 요소의 출력과 다음 구성 요소의 입력 간의 연결 및 이 연결 사이의 데이터에서 수행되는 모든 데이터 변환을 다룹니다. 데이터 흐름 방향은 출력을 받을 구성 요소를 지정하는 논리가 포함된 선행 제약 조건에 의해 결정됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 태스크에는 DDL 실행 태스크, Analysis Services 처리 태스크 및 데이터 마이닝 쿼리 태스크가 있습니다. 이러한 각 태스크에 대해 메일 보내기 작업을 사용하여 관리자에게 작업 결과가 포함된 전자 메일 메시지를 보낼 수 있습니다.  
  
## <a name="the-execute-ddl-task"></a>DDL 실행 태스크  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 DDL 실행 태스크를 사용하여 DDL 스크립트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버로 직접 보내고 자동으로 실행할 수 있습니다. 이렇게 하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 내에서 백업, 복원 또는 동기화 작업을 수행할 수 있습니다. 패키지는 앞에서 설명한 제어 흐름 요소와 데이터 흐름 요소로 구성되어 있으며 이러한 모든 요소는 태스크에 추가할 수 있는 다른 DDL 문과 같이 **run regularly**여야 합니다. 여기서 설명하는 태스크는 종종 야간에 실행되기 때문에 예약 애플리케이션에서 쉽게 실행할 수 있는 패키지가 있으면 특히 유용합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에이전트를 사용하여 언제든지 패키지가 실행되도록 예약할 수 있습니다. 이 태스크의 구현 방법은 [Analysis Services DDL 실행 태스크](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)를 참조하세요.  
  
## <a name="analysis-services-processing-task"></a>Analysis Services 처리 태스크  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 Analysis Services 처리 태스크를 사용하여 원본 관계형 데이터베이스를 정기적으로 업데이트할 때 자동으로 큐브를 새 정보로 채울 수 있습니다. Analysis Services 처리 태스크를 사용하여 차원, 큐브 또는 파티션 수준에서 처리할 수 있습니다. 작업 요구 사항에 따라 처리 자체의 유형을 **incremental** 또는 **full**로 선택할 수 있습니다. 증분 처리는 새 데이터를 추가하고 충분히 다시 계산하여 대상을 최신 상태로 유지하는 반면 전체 처리는 기존 데이터를 삭제하여 대상을 완전히 다시 로드 및 계산합니다. 전체 처리는 많은 시간이 소요되지만 보다 완전합니다. 이 태스크의 구현 방법은 [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md)을 참조하십시오.  
  
## <a name="data-mining-query-task"></a>데이터 마이닝 쿼리 태스크  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 데이터 마이닝 쿼리 태스크를 사용하여 마이닝 모델에서 정보를 추출 및 저장할 수 있습니다. 이러한 정보는 종종 관계형 데이터베이스에 저장되며 대상 마케팅 캠페인을 위해 잠재적인 고객 목록을 구분하는 데 사용할 수 있습니다. 데이터 마이닝을 통해 고객의 가치 및 고객이 특정 마케팅 전략에 응답할 확률을 식별할 수 있습니다. 또한 데이터 마이닝 쿼리 태스크를 사용하여 데이터를 원하는 형식으로 추출 및 수정할 수 있습니다. 이 태스크의 구현 방법은 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [파티션 처리 대상](../../integration-services/data-flow/partition-processing-destination.md)   
 [차원 처리 대상](../../integration-services/data-flow/dimension-processing-destination.md)   
 [데이터 마이닝 쿼리 변환](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)   
 [다차원 모델 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
  
  
