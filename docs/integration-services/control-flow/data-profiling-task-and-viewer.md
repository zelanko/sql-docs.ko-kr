---
title: "데이터 프로 파일링 태스크 및 뷰어 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling task [Integration Services], about data profiling
- data profiling
- profiling data
ms.assetid: 756840e3-aa09-45cd-9951-1a17af4b5925
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7738775f08124a54765b3597af992a74d63aaf33
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="data-profiling-task-and-viewer"></a>데이터 프로파일링 태스크 및 뷰어
  데이터 프로파일링 태스크는 데이터 추출, 변환 및 로드 프로세스 내에서 데이터 프로파일링 기능을 제공합니다. 데이터 프로파일링 태스크를 사용하면 다음과 같은 이점이 있습니다.  
  
-   보다 효과적으로 원본 데이터 분석  
  
-   원본 데이터에 대한 이해도 향상  
  
-   데이터 웨어하우스에 노출되기 전에 데이터 품질 문제 방지  
  
> [!IMPORTANT]  
>  데이터 프로파일링 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 저장된 데이터만 사용할 수 있습니다. 이 태스크는 타사 또는 파일 기반 데이터 원본을 사용할 수 없습니다.  
  
## <a name="data-profiling-overview"></a>데이터 프로파일링 개요  
 데이터 품질은 모든 비즈니스에서 중요합니다. 기업에서는 분석 및 비즈니스 인텔리전스 시스템을 자체 트랜잭션 시스템 위에 빌드하므로 핵심 성과 지표 및 데이터 마이닝 예측의 안정성은 기반으로 하고 있는 데이터의 유효성에 따라 전적으로 달라집니다. 비즈니스 의사 결정에서 유효한 데이터의 중요성이 증가하고 있지만 이러한 데이터의 유효성을 확인하는 문제의 중요성 또한 증가하고 있습니다. 데이터는 실로 다양한 시스템 및 출처와 많은 사용자로부터 기업으로 계속 흘러 들어오고 있습니다.  
  
 데이터 품질의 메트릭은 특정 도메인이나 응용 프로그램과 관련되어 있으므로 정의하기 어려울 수 있습니다. 데이터 품질을 정의하는 일반적인 방법 중 하나가 데이터 프로파일링입니다.  
  
 데이터 프로필은 다음을 포함할 수 있는 데이터에 대한 집계 통계 모음입니다.  
  
-   Customer 테이블의 행 수  
  
-   State 열의 고유 값 수  
  
-   Zip 열의 Null 값 또는 누락된 값 수  
  
-   City 열의 값 분포  
  
-   State 열의 Zip 열에 대한 함수 종속성 수준(시/도는 지정된 우편 번호 값에 대해 항상 같아야 함)  
  
 데이터 프로필이 제공하는 통계를 통해 원본 데이터를 사용하여 발생할 수 있는 품질 문제를 효과적으로 최소화하기 위해 필요한 정보를 얻을 수 있습니다.  
  
## <a name="integration-services-and-data-profiling"></a>Integration Services 및 데이터 프로파일링  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 데이터 프로파일링 프로세스는 다음 단계로 구성됩니다.  
  
 **1단계: 데이터 프로파일링 태스크 설정**  
 데이터 프로파일링 태스크는 계산하려는 프로필을 구성하기 위해 사용하는 태스크입니다. 데이터 프로파일링 태스크를 포함하는 패키지를 실행하여 프로필을 계산합니다. 이 태스크는 프로필 출력을 XML 형식으로 파일이나 패키지 변수에 저장합니다.  
  
 **자세한 내용:** [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)  
  
 **2단계: 데이터 프로파일링 태스크가 계산하는 프로필 검토**  
 데이터 프로파일링 태스크가 계산하는 데이터 프로필을 보려면 출력을 파일로 보낸 다음 데이터 프로필 뷰어를 사용합니다. 이 뷰어는 선택적 드릴다운 기능과 함께 요약 및 세부 정보 형식으로 프로필 출력을 표시하는 독립 실행형 유틸리티입니다.  
  
 **자세한 내용:** [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)  
  
### <a name="addition-of-conditional-logic-to-the-data-profiling-workflow"></a>데이터 프로파일링 워크플로에 조건부 논리 추가  
 데이터 프로파일링 태스크에는 조건부 논리를 사용하여 프로필 출력에 따라 해당 태스크를 다운스트림 태스크에 연결할 수 있는 기본 제공 기능이 없습니다. 그러나 스크립트 태스크에서 약간의 프로그래밍 작업을 수행하여 이 논리를 손쉽게 추가할 수 있습니다. 예를 들어 스크립트 태스크는 데이터 프로파일링 태스크의 출력 파일에 대해 XPath 쿼리를 수행할 수 있습니다. 이 쿼리에서는 특정 열의 Null 값 비율이 특정 임계값을 초과하는지 여부를 확인할 수 있습니다. 해당 비율이 임계값을 초과하는 경우 패키지를 중단하고 원본 데이터에서 문제를 해결한 다음 계속할 수 있습니다. 자세한 내용은 [패키지 워크플로에 데이터 프로파일링 태스크 포함](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 [데이터 프로파일러 스키마](http://go.microsoft.com/fwlink/?LinkId=251524)  
  
  

