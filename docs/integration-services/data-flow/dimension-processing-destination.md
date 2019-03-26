---
title: 차원 처리 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dimensionprocessingdest.f1
- sql13.dts.designer.dimprocessingtransformation.connection.f1
- sql13.dts.designer.dimprocessingtransformation.mappings.f1
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 538799037cd634f48a0eb2a2d2138fef9ded0c5b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280727"
---
# <a name="dimension-processing-destination"></a>차원 처리 대상
  차원 처리 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 차원을 로드하고 처리합니다. 차원에 대한 자세한 내용은 [차원&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 차원 처리 대상에는 다음 기능이 포함됩니다.  
  
-   증분, 전체 또는 업데이트 처리를 수행하기 위한 옵션  
  
-   차원 처리 중에 오류를 무시하거나 지정된 오류 개수 이후에 프로세스가 중지되는지 여부를 지정하기 위한 오류 구성  
  
-   입력 열을 차원 테이블의 열로 매핑  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 처리하는 방법에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>차원 처리 대상 구성  
 차원 처리 대상은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결하거나 대상에서 처리되는 차원이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 이 대상은 하나의 입력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="dimension-processing-destination-editor-connection-manager-page"></a>차원 처리 대상 편집기(연결 관리자 페이지)
   **차원 처리 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 대한 연결을 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **Connection manager**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다.  
  
 **새로 만들기**  
 **Analysis Services 연결 관리자 추가** 대화 상자를 사용하면 새 연결을 만들 수 있습니다.  
  
 **사용 가능한 차원 목록**  
 처리할 차원을 선택합니다.  
  
 **처리 방법**  
 목록에서 선택한 차원에 적용할 처리 방법을 선택합니다. 이 옵션의 기본값은 **전체**입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**추가(증분)**|차원의 증분 처리를 수행합니다.|  
|**전체**|차원의 전체 처리를 수행합니다.|  
|**Update**|차원의 업데이트 처리를 수행합니다.|  
  
## <a name="dimension-processing-destination-editor-mappings-page"></a>차원 처리 대상 편집기(매핑 페이지)
  **차원 처리 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 차원 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 입력 열을 대상 열에 매핑합니다.  
  
 **사용 가능한 대상 열**  
 사용 가능한 대상 열의 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 대상 열을 입력 열에 매핑합니다.  
  
 **입력 열**  
 위 테이블에서 선택한 입력 열을 표시합니다. **사용 가능한 입력 열**의 목록을 사용하여 매핑을 변경할 수 있습니다.  
  
 **대상 열**  
 매핑 여부에 관계없이 사용 가능한 각 대상 열을 표시합니다.  
  
## <a name="dimension-processing-destination-editor-advanced-page"></a>차원 처리 대상 편집기(고급 페이지)
  **차원 처리 대상 편집기** 대화 상자의 **고급** 페이지를 사용하여 오류 처리 방법을 구성할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **기본 오류 구성 사용**  
 기본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 오류 처리를 사용할지 여부를 지정합니다. 기본적으로 이 값은 **True**입니다.  
  
 **키 오류 동작**  
 사용할 수 없는 키 값이 있는 레코드의 처리 방법을 지정합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**ConvertToUnknown**|사용할 수 없는 키 값을 **UnknownMember** 값으로 변환합니다.|  
|**DiscardRecord**|레코드를 삭제합니다.|  
  
 **오류 무시**  
 오류를 무시하도록 지정합니다.  
  
 **오류 발생 시 중지**  
 오류가 발생하면 처리를 중지하도록 지정합니다.  
  
 **오류 개수**  
 **오류 발생 시 중지**를 선택한 경우 처리를 중지하는 데 기준이 되는 오류 임계값을 지정합니다.  
  
 **오류 시 수행할 동작**  
 **오류 발생 시 중지**를 선택한 경우 오류 임계값에 도달했을 때 수행할 동작을 지정합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**StopProcessing**|처리를 중지합니다.|  
|**StopLogging**|오류 기록을 중지합니다.|  
  
 **키를 찾을 수 없는 경우**  
 키를 찾을 수 없을 때 수행할 동작을 지정합니다. 기본적으로 이 값은 **ReportAndContinue**입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **중복 키**  
 중복 키 오류가 발생할 때 수행할 동작을 지정합니다. 기본적으로 이 값은 **IgnoreError**입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **Null 키가 알 수 없는 상태로 변환된 경우**  
 Null 키가 **UnknownMember** 값으로 변환된 경우 수행할 동작을 지정합니다. 기본적으로 이 값은 **IgnoreError**입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **Null 키가 허용되지 않는 경우**  
 Null 키가 허용되지 않는데 Null 키가 있는 경우에 수행할 동작을 지정합니다. 기본적으로 이 값은 **ReportAndContinue**입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **오류 로그 경로**  
 오류 로그의 경로를 입력하거나 **찾아보기(...)** 단추를 클릭하여 대상을 선택합니다.  
  
 **찾아보기(...)**  
 오류 로그의 경로를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
