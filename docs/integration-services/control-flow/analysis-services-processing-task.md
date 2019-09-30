---
title: Analysis Services 처리 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asprocessingtask.f1
- sql13.dts.designer.asprocessingtask.general.f1
- sql13.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92e0656fd3625f2b93a1e097d2f81291056d01cf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298464"
---
# <a name="analysis-services-processing-task"></a>Analysis Services 처리 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크는 테이블 형식 모델, 큐브, 차원 및 마이닝 모델과 같은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 처리합니다.  
  
 테이블 형식 모델을 처리할 때는 다음 사항에 유의해야 합니다.  
  
-   테이블 형식 모델에서는 영향 분석을 수행할 수 없습니다.  
  
-   조각 모음 처리 및 다시 계산 처리와 같은 테이블 형식 모드에 대한 일부 처리 옵션은 표시되지 않습니다. DDL 실행 태스크를 사용하여 이러한 함수를 수행할 수 있습니다.  
  
-   인덱스 처리 및 업데이트 처리 옵션은 테이블 형식 모델에 적합하지 않으며 사용하지 않아야 합니다.  
  
-   테이블 형식 모델에서는 일괄 설정이 무시됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 DDL(데이터 정의 언어) 문과 데이터 마이닝 예측 쿼리 실행 등의 비즈니스 인텔리전스 태스크를 수행하는 많은 태스크가 있습니다. 관련 비즈니스 인텔리전스 태스크에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Analysis Services DDL 실행 태스크](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [데이터 마이닝 쿼리 태스크](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="object-processing"></a>개체 처리  
 동시에 여러 개의 개체를 처리할 수 있습니다. 여러 개의 개체를 처리하는 경우 일괄 처리의 모든 개체 처리에 적용되는 설정을 정의합니다.  
  
 일괄 처리의 개체를 순서대로 또는 병렬로 처리할 수 있습니다. 처리 시퀀스가 중요한 개체가 일괄 처리에 포함되어 있지 않으면 병렬 처리를 사용하여 처리 속도를 증가시킬 수 있습니다. 일괄 처리의 개체가 병렬로 처리되는 경우 태스크에서 병렬로 처리할 개체 수를 결정하도록 구성하거나 동시에 처리할 개체 수를 직접 지정할 수 있습니다. 개체가 순서대로 처리되는 경우 한 트랜잭션에 모든 개체를 나열하거나 일괄 처리의 각 개체에 대해 별도의 트랜잭션을 사용하여 일괄 처리에 트랜잭션 특성을 설정할 수 있습니다.  
  
 분석 개체를 처리할 때 종속 개체를 함께 처리할 수도 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크에는 선택한 개체 외에 모든 종속 개체를 처리하는 옵션이 있습니다.  
  
 일반적으로 팩트 테이블을 처리하기 전에 차원 테이블을 처리합니다. 차원 테이블을 처리하기 전에 팩트 테이블을 처리하려고 할 경우 오류가 발생할 수 있습니다.  
  
 이 태스크를 사용하여 차원 키 오류 처리를 구성할 수도 있습니다. 예를 들어 이 태스크는 오류를 무시하거나 지정한 수의 오류가 발생한 후 중지될 수 있습니다. 기본 오류 구성을 태스크에 사용하거나 사용자 지정 오류 구성을 생성할 수 있습니다. 사용자 지정 오류 구성에서는 태스크의 오류 처리 방법과 오류 조건을 지정합니다. 예를 들어 4번째 오류가 발생한 후 태스크 실행을 중지하도록 지정하거나 태스크에서 **Null** 키 값을 처리하는 방법을 지정할 수 있습니다. 사용자 지정 오류 구성에 오류 로그 경로를 포함할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 만든 분석 개체만 처리할 수 있습니다.  
  
 이 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터를 로드하는 대량 삽입 태스크나 데이터를 테이블에 로드하는 데이터 흐름을 구현하는 데이터 흐름 태스크와 함께 자주 사용됩니다. 예를 들어 OLTP(온라인 트랜잭션 데이터베이스) 데이터베이스에서 데이터를 추출하여 데이터 웨어하우스의 팩트 테이블에 로드하는 데이터 흐름이 데이터 흐름 태스크에 포함될 수 있습니다. 그런 다음 데이터 웨어하우스에 작성된 큐브 처리를 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크가 호출됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 태스크는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
## <a name="error-handling"></a>오류 처리  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Analysis Services 처리 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Analysis Services 처리 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
## <a name="analysis-services-processing-task-editor-general-page"></a>Analysis Services 처리 태스크 편집기(일반 페이지)
  **Analysis Services 처리 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 Analysis Services 처리 태스크를 명명 및 설명할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **이름**  
 Analysis Services 처리 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 Analysis Services 처리 태스크에 대한 설명을 입력합니다.  
  
## <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Analysis Services 처리 태스크 편집기(Analysis Services 페이지)
  **Analysis Services 처리 태스크 편집기** 대화 상자의 **Analysis Services** 페이지를 사용하여 Analysis Services 연결 관리자를 지정하고, 처리할 분석 개체를 선택하고, 처리 및 오류 처리 옵션을 설정할 수 있습니다.  
  
 테이블 형식 모델을 처리할 때는 다음 사항에 유의해야 합니다.  
  
1.  테이블 형식 모델에서는 영향 분석을 수행할 수 없습니다.  
  
2.  조각 모음 처리 및 다시 계산 처리와 같은 테이블 형식 모드에 대한 일부 처리 옵션은 표시되지 않습니다. DDL 실행 태스크를 사용하여 이러한 함수를 수행할 수 있습니다.  
  
3.  인덱스 처리와 같은 제공되는 일부 처리 옵션은 테이블 형식 모델에 적합하지 않으며 사용하지 않아야 합니다.  
  
4.  테이블 형식 모델에서는 일괄 설정이 무시됩니다.  
  
### <a name="options"></a>옵션  
 **Analysis Services 연결 관리자**  
 목록에서 기존 Analysis Services 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다.  
  
 **새로 만들기**  
 새 Analysis Services 연결 관리자를 만듭니다.  
  
 **관련 항목:** [Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md), [Analysis Services 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **개체 목록**  
 |속성|설명|  
|--------------|-----------------|  
|**Object Name**|지정한 개체 이름을 나열합니다.|  
|**형식**|지정한 개체의 유형을 나열합니다.|  
|**처리 옵션**|목록에서 처리 옵션을 선택합니다.<br /><br /> **관련 항목**: [다차원 모델 처리&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services)|  
|**설정**|지정한 개체에 대한 처리 설정을 나열합니다.|  
  
 **추가**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 목록에 추가합니다.  
  
 **제거**  
 개체를 선택한 다음 **삭제**를 클릭합니다.  
  
 **영향 분석**  
 선택한 개체에 대한 영향 분석을 수행합니다.  
  
 **관련 항목:** [영향 분석 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](https://msdn.microsoft.com/library/208268eb-4e14-44db-9c64-6f74b776adb6)  
  
 **일괄 처리 설정 요약**  
 |속성|설명|  
|--------------|-----------------|  
|**처리 순서**|개체가 순차적으로 또는 일괄 처리 방식으로 처리되는지 여부를 지정합니다. 병렬 처리가 사용되면 동시에 처리할 개체 수를 지정합니다.|  
|**트랜잭션 모드**|순차적 처리를 위한 트랜잭션 모드를 지정합니다.|  
|**차원 오류**|오류 발생 시의 태스크 동작을 지정합니다.|  
|**차원 키 오류 로그 경로**|오류가 기록되는 파일의 경로를 지정합니다.|  
|**영향을 받는 개체 처리**|종속 개체나 영향을 받는 개체도 처리되는지 여부를 나타냅니다.|  
  
 **설정 변경**  
 처리 옵션 및 차원 키의 오류 처리를 변경합니다.  
  
 **관련 항목:** [설정 변경 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](https://msdn.microsoft.com/library/0041e042-d7ce-48f9-a690-a6dc65471ff3)  
  
