---
title: Analysis Services 처리 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 02023482a2f3537872b50ac70f8bfd68d2128e1b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379131"
---
# <a name="analysis-services-processing-task"></a>Analysis Services 처리 태스크
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크는 테이블 형식 모델, 큐브, 차원 및 마이닝 모델과 같은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 처리합니다.  
  
 테이블 형식 모델을 처리할 때는 다음 사항에 유의해야 합니다.  
  
-   테이블 형식 모델에서는 영향 분석을 수행할 수 없습니다.  
  
-   조각 모음 처리 및 다시 계산 처리와 같은 테이블 형식 모드에 대한 일부 처리 옵션은 표시되지 않습니다. DDL 실행 태스크를 사용하여 이러한 함수를 수행할 수 있습니다.  
  
-   인덱스 처리 및 업데이트 처리 옵션은 테이블 형식 모델에 적합하지 않으며 사용하지 않아야 합니다.  
  
-   테이블 형식 모델에서는 일괄 설정이 무시됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 DDL(데이터 정의 언어) 문과 데이터 마이닝 예측 쿼리 실행 등의 비즈니스 인텔리전스 태스크를 수행하는 많은 태스크가 있습니다. 관련 비즈니스 인텔리전스 태스크에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services DDL 실행 태스크](analysis-services-execute-ddl-task.md)  
  
-   [데이터 마이닝 쿼리 태스크](data-mining-query-task.md)  
  
## <a name="object-processing"></a>개체 처리  
 동시에 여러 개의 개체를 처리할 수 있습니다. 여러 개의 개체를 처리하는 경우 일괄 처리의 모든 개체 처리에 적용되는 설정을 정의합니다.  
  
 일괄 처리의 개체를 순서대로 또는 병렬로 처리할 수 있습니다. 처리 시퀀스가 중요한 개체가 일괄 처리에 포함되어 있지 않으면 병렬 처리를 사용하여 처리 속도를 증가시킬 수 있습니다. 일괄 처리의 개체가 병렬로 처리되는 경우 태스크에서 병렬로 처리할 개체 수를 결정하도록 구성하거나 동시에 처리할 개체 수를 직접 지정할 수 있습니다. 개체가 순서대로 처리되는 경우 한 트랜잭션에 모든 개체를 나열하거나 일괄 처리의 각 개체에 대해 별도의 트랜잭션을 사용하여 일괄 처리에 트랜잭션 특성을 설정할 수 있습니다.  
  
 분석 개체를 처리할 때 종속 개체를 함께 처리할 수도 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크에는 선택한 개체 외에 모든 종속 개체를 처리하는 옵션이 있습니다.  
  
 일반적으로 팩트 테이블을 처리하기 전에 차원 테이블을 처리합니다. 차원 테이블을 처리하기 전에 팩트 테이블을 처리하려고 할 경우 오류가 발생할 수 있습니다.  
  
 이 태스크를 사용하여 차원 키 오류 처리를 구성할 수도 있습니다. 예를 들어 이 태스크는 오류를 무시하거나 지정한 수의 오류가 발생한 후 중지될 수 있습니다. 기본 오류 구성을 태스크에 사용하거나 사용자 지정 오류 구성을 생성할 수 있습니다. 사용자 지정 오류 구성에서는 태스크의 오류 처리 방법과 오류 조건을 지정합니다. 예를 들어 4번째 오류가 발생한 후 태스크 실행을 중지하도록 지정하거나 태스크에서 **Null** 키 값을 처리하는 방법을 지정할 수 있습니다. 사용자 지정 오류 구성에 오류 로그 경로를 포함할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 만든 분석 개체만 처리할 수 있습니다.  
  
 이 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터를 로드하는 대량 삽입 태스크나 데이터를 테이블에 로드하는 데이터 흐름을 구현하는 데이터 흐름 태스크와 함께 자주 사용됩니다. 예를 들어 OLTP(온라인 트랜잭션 데이터베이스) 데이터베이스에서 데이터를 추출하여 데이터 웨어하우스의 팩트 테이블에 로드하는 데이터 흐름이 데이터 흐름 태스크에 포함될 수 있습니다. 그런 다음 데이터 웨어하우스에 작성된 큐브 처리를 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크가 호출됩니다.  
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
## <a name="error-handling"></a>오류 처리  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Analysis Services 처리 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services 처리 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Analysis Services 처리 태스크 편집기&#40;Analysis Services 페이지&#41;](../analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Analysis Services 처리 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  
