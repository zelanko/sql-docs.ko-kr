---
title: 파티션 처리 대상 편집기 (고급 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.advanced.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 2039ee0f-069d-479d-90b2-2a12481b1162
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: de7c84a463d15e3260cc64c53ba1f82c6808dd93
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056781"
---
# <a name="partition-processing-destination-editor-advanced-page"></a>파티션 처리 대상 편집기(고급 페이지)
  **파티션 처리 대상 편집기** 대화 상자의 **고급** 페이지를 사용하여 오류 처리 방법을 구성할 수 있습니다.  
  
 파티션 처리 대상에 대한 자세한 내용은 [Partition Processing Destination](data-flow/partition-processing-destination.md)을 참조하세요.  
  
> [!NOTE]  
>  여기에서 설명하는 태스크는 Analysis Services 테이블 형식 모델에 적용되지 않습니다.  테이블 형식 모델의 경우 입력 열을 파티션 열에 매핑할 수 없습니다. 대신 [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) 를 사용하여 파티션을 처리할 수 있습니다.  
  
## <a name="options"></a>변수  
 **기본 오류 구성 사용**  
 기본 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 오류 처리를 사용할지 여부를 지정합니다. 기본적으로 이 값은 `True`입니다.  
  
 **키 오류 동작**  
 사용할 수 없는 키 값이 있는 레코드의 처리 방법을 지정합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|사용할 수 없는 키 값을 Unknown 값으로 변환합니다.|  
|**DiscardRecord**|레코드를 삭제합니다.|  
  
 **오류 무시**  
 오류를 무시하도록 지정합니다.  
  
 **오류 발생 시 중지**  
 오류가 발생하면 처리를 중지하도록 지정합니다.  
  
 **오류 개수**  
 **오류 발생 시 중지**를 선택한 경우 처리를 중지하는 데 기준이 되는 오류 임계값을 지정합니다.  
  
 **오류 시 수행할 동작**  
 **오류 발생 시 중지**를 선택한 경우 오류 임계값에 도달했을 때 수행할 동작을 지정합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**StopProcessing**|처리를 중지합니다.|  
|**StopLogging**|오류 기록을 중지합니다.|  
  
 **키를 찾을 수 없는 경우**  
 키를 찾을 수 없을 때 수행할 동작을 지정합니다. 기본적으로 이 값은 **ReportAndContinue**입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **중복 키**  
 중복 키 오류가 발생할 때 수행할 동작을 지정합니다. 기본적으로 이 값은 **IgnoreError**입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **Null 키가 알 수 없는 상태로 변환된 경우**  
 Null 키가 Unknown 값으로 변환된 경우 수행할 동작을 지정합니다. 기본적으로 이 값은 **IgnoreError**입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **Null 키가 허용되지 않는 경우**  
 Null 키가 허용되지 않는데 Null 키가 있는 경우에 수행할 동작을 지정합니다. 기본적으로 이 값은 **ReportAndContinue**입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**IgnoreError**|오류를 무시하고 처리를 계속합니다.|  
|**ReportAndContinue**|오류를 보고하고 처리를 계속합니다.|  
|**ReportAndStop**|오류를 보고하고 처리를 중지합니다.|  
  
 **오류 로그 경로**  
 오류 로그의 경로를 입력하거나 찾아보기 단추 **(...)** 를 사용하여 대상을 선택합니다.  
  
 **찾아보기(...)**  
 오류 로그의 경로를 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [파티션 처리 대상 편집기&#40;매핑 페이지&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)  
  
  
