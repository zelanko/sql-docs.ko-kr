---
title: Analysis Services 처리 태스크 편집기 (Analysis Services 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing Task Editor
ms.assetid: 5612be78-57cf-4e4e-92cf-6bfa9f971040
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 386854ec9a20931571ececf4bca943f95fc0dbf7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62836457"
---
# <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Analysis Services 처리 태스크 편집기(Analysis Services 페이지)
  **Analysis Services 처리 태스크 편집기** 대화 상자의 **Analysis Services** 페이지를 사용하여 Analysis Services 연결 관리자를 지정하고, 처리할 분석 개체를 선택하고, 처리 및 오류 처리 옵션을 설정할 수 있습니다.  
  
 테이블 형식 모델을 처리할 때는 다음 사항에 유의해야 합니다.  
  
1.  테이블 형식 모델에서는 영향 분석을 수행할 수 없습니다.  
  
2.  조각 모음 처리 및 다시 계산 처리와 같은 테이블 형식 모드에 대한 일부 처리 옵션은 표시되지 않습니다. DDL 실행 태스크를 사용하여 이러한 함수를 수행할 수 있습니다.  
  
3.  인덱스 처리와 같은 제공되는 일부 처리 옵션은 테이블 형식 모델에 적합하지 않으며 사용하지 않아야 합니다.  
  
4.  테이블 형식 모델에서는 일괄 설정이 무시됩니다.  
  
 이 태스크에 대한 자세한 내용은 [Analysis Services Processing Task](control-flow/analysis-services-processing-task.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **Analysis Services 연결 관리자**  
 목록에서 기존 Analysis Services 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다.  
  
 **새로 만들기**  
 새 Analysis Services 연결 관리자를 만듭니다.  
  
 **관련 항목:** [Analysis Services 연결 관리자](connection-manager/analysis-services-connection-manager.md), [Analysis Services 연결 관리자 추가 대화 상자 UI 참조](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **개체 목록**  
 |속성|Description|  
|--------------|-----------------|  
|**Object Name**|지정한 개체 이름을 나열합니다.|  
|**형식**|지정한 개체의 유형을 나열합니다.|  
|**처리 옵션**|목록에서 처리 옵션을 선택합니다.<br /><br /> **관련 항목**: [다차원 모델 개체 처리](../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)|  
|**설정**|지정한 개체에 대한 처리 설정을 나열합니다.|  
  
 **추가**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체를 목록에 추가합니다.  
  
 **제거**  
 개체를 선택한 다음 **삭제**를 클릭합니다.  
  
 **영향 분석**  
 선택한 개체에 대한 영향 분석을 수행합니다.  
  
 **관련 항목:** [영향 분석 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](../../2014/analysis-services/impact-analysis-dialog-box-analysis-services-multidimensional-data.md)  
  
 **일괄 처리 설정 요약**  
 |속성|Description|  
|--------------|-----------------|  
|**처리 순서**|개체가 순차적으로 또는 일괄 처리 방식으로 처리되는지 여부를 지정합니다. 병렬 처리가 사용되면 동시에 처리할 개체 수를 지정합니다.|  
|**트랜잭션 모드**|순차적 처리를 위한 트랜잭션 모드를 지정합니다.|  
|**차원 오류**|오류 발생 시의 태스크 동작을 지정합니다.|  
|**차원 키 오류 로그 경로**|오류가 기록되는 파일의 경로를 지정합니다.|  
|**영향을 받는 개체 처리**|종속 개체나 영향을 받는 개체도 처리되는지 여부를 나타냅니다.|  
  
 **설정 변경**  
 처리 옵션 및 차원 키의 오류 처리를 변경합니다.  
  
 **관련 항목:** [설정 변경 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](../../2014/analysis-services/change-settings-dialog-box-analysis-services-multidimensional-data.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services 처리 태스크 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [Analysis Services DDL 실행 태스크](control-flow/analysis-services-execute-ddl-task.md)  
  
  
