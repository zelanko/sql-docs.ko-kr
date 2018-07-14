---
title: 다차원 모델링 (Adventure Works 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tutorials [Analysis Services]
- Analysis Services, tutorials
ms.assetid: db55e226-601a-4026-8651-573195555a59
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 206105b0dda4da406abf46f70f27b511dee99e0d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220353"
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>다차원 모델링(Adventure Works 자습서)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 자습서입니다. 이 자습서의 모든 예에서는 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 라는 가상 회사에서 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 프로젝트를 개발 및 배포하는 방법을 설명합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 다음 항목을 배웁니다.  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 내의 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]프로젝트에서 데이터 원본, 데이터 원본 뷰, 차원, 특성, 특성 관계, 계층 및 큐브를 정의하는 방법  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 배포하여 큐브 및 차원 데이터를 보는 방법과 배포된 개체를 처리하여 기본 데이터 원본의 데이터로 채우는 방법  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트에서 측정값, 차원, 계층, 특성 및 측정값 그룹을 수정하는 방법과 개발 서버에서 배포된 큐브에 증분 변경을 배포하는 방법  
  
-   큐브 내에서 계산, KPI(핵심 성과 지표), 동작, 큐브 뷰, 번역 및 보안 역할을 정의하는 방법  
  
 이 단원에 대한 컨텍스트를 더 잘 이해할 수 있도록 이 자습서와 함께 시나리오 설명이 제공됩니다. 자세한 내용은 [Analysis Services Tutorial Scenario](analysis-services-tutorial-scenario.md)을 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 자습서의 모든 단원을 완료하려면 예제 데이터, 예제 프로젝트 파일 및 소프트웨어가 있어야 합니다. 이 자습서의 필수 구성 요소를 찾아서 설치하는 방법은 [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](install-sample-data-and-projects.md)를 참조하십시오.  
  
 이 자습서를 성공적으로 완료하려면 이 외에도 다음과 같은 사용 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 컴퓨터에서 Administrators 로컬 그룹의 멤버이거나 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에서 서버 관리 역할의 멤버여야 합니다.  
  
-   **AdventureWorksDW2012** 예제 데이터베이스에 대한 읽기 권한이 있어야 합니다. 이 예제 데이터베이스는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 릴리스에 사용할 수 있습니다.  
  
## <a name="lessons"></a>단원  
 이 자습서에는 다음 단원이 포함되어 있습니다.  
  
|단원|소요되는 예상 시간|  
|------------|--------------------------------|  
|[1단원: Analysis Services 프로젝트 내의 데이터 원본 뷰 정의](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15분|  
|[2단원: 큐브 정의 및 배포](lesson-2-defining-and-deploying-a-cube.md)|30분|  
|[3단원: 측정값, 특성 및 계층 수정](lesson-3-modifying-measures-attributes-and-hierarchies.md)|45분|  
|[4단원: 고급 특성 및 차원 속성 정의](lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120분|  
|[5단원: 차원과 측정값 그룹의 관계 정의](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45분|  
|[6단원: 계산 정의](lesson-6-defining-calculations.md)|45분|  
|[7 단원: 핵심 성과 지표를 정의 &#40;Kpi&#41;](lesson-7-defining-key-performance-indicators-kpis.md)|30분|  
|[8단원: 동작 정의](lesson-8-defining-actions.md)|30분|  
|[9단원: 큐브 뷰 및 번역 정의](lesson-9-defining-perspectives-and-translations.md)|30분|  
|[10단원: 관리자 역할 정의](lesson-10-defining-administrative-roles.md)|15분|  
  
> [!NOTE]  
>  이 자습서에서 만들 큐브 데이터베이스는 codeplex 사이트에서 다운로드할 수 있는 Adventure Works 예제 데이터베이스의 일부인 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다차원 모델 프로젝트의 단순화된 버전입니다. Adventure Works 다차원 데이터베이스의 자습서 버전은 바로 익히려는 특정 기술에 더 집중하도록 단순화되어 있습니다. 이 자습서를 끝낸 후에는 직접 다차원 모델 프로젝트를 탐색하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다차원 모델링에 대한 이해를 높이는 것이 좋습니다.  
  
## <a name="next-step"></a>다음 단계  
 자습서를 시작하려면 첫 번째 단원인 [Lesson 1: Defining a Data Source View within an Analysis Services Project](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)로 이동하십시오.  
  
  
