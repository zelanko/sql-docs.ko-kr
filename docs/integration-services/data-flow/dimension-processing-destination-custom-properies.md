---
title: 차원 처리 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f46acb401bf04e9b0445c452e26d69de42a2d94
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292832"
---
# <a name="dimension-processing-destination-custom-properies"></a>차원 처리 대상 사용자 지정 속성

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  차원 처리 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 차원 처리 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 연결 문자열입니다.|  
|KeyDuplicate|Integer(열거형)|UseDefaultConfiguration이 **False**일 때 중복 키 오류를 처리하는 방법을 나타내는 값입니다. 가능한 값은 **IgnoreError** (0), **ReportAndContinue** (1) 및 **ReportAndStop** (2)입니다. 이 속성의 기본값은 **IgnoreError** (0)입니다.|  
|KeyErrorAction|Integer(열거형)|UseDefaultConfiguration이 **False**일 때 키 오류를 처리하는 방법을 나타내는 값입니다. 가능한 값은 **ConvertToUnknown** (0) 및 **DiscardRecord** (1)입니다. 이 속성의 기본값은 **ConvertToUnknown** (0)입니다.|  
|KeyErrorLimit|정수|UseDefaultConfiguration이 **False**일 때 사용하도록 설정된 키 오류의 상한값입니다.|  
|KeyErrorLimitAction|Integer(열거형)|UseDefaultConfiguration이 **False**일 때 **KeyErrorLimit** 에 도달하면 수행할 동작을 나타내는 값입니다. 가능한 값은 **StopLogging** (1) 및 **StopProcessing** (0)입니다. 이 속성의 기본값은 **StopProcessing** (0)입니다.|  
|KeyErrorLogFile|String|UseDefaultConfiguration이 **False**일 때 오류 로그 파일의 경로 및 파일 이름입니다.|  
|KeyNotFound|Integer(열거형)|UseDefaultConfiguration이 **False**일 때 누락 키 오류를 처리하는 방법을 나타내는 값입니다. 가능한 값은 **IgnoreError** (0), **ReportAndContinue** (1) 및 **ReportAndStop** (2)입니다. 이 속성의 기본값은 **IgnoreError** (0)입니다.|  
|NullKeyConvertedToUnknown|Integer(열거형)|UseDefaultConfiguration이 **False**일 때 알 수 없는 값으로 변환된 null 키를 처리하는 방법을 나타내는 값입니다. 가능한 값은 **IgnoreError** (0), **ReportAndContinue** (1) 및 **ReportAndStop** (2)입니다. 이 속성의 기본값은 **IgnoreError** (0)입니다.|  
|NullKeyNotAllowed|Integer(열거형)|UseDefaultConfiguration이 **False**일 때 허용되지 않는 null을 처리하는 방법을 나타내는 값입니다. 가능한 값은 **IgnoreError** (0), **ReportAndContinue** (1) 및 **ReportAndStop** (2)입니다. 이 속성의 기본값은 **IgnoreError** (0)입니다.|  
|ProcessType|Integer(열거형)|변환에서 사용하는 차원 처리의 유형입니다. 값은 **ProcessAdd** (1)(증분), **ProcessFull** (0) 및 **ProcessUpdate** (2)입니다.|  
|UseDefaultConfiguration|Boolean|변환에서 기본 오류 구성을 사용하는지 여부를 지정하는 값입니다. 이 속성이 **False**인 경우 변환에 오류 처리에 대한 정보가 포함됩니다.|  
  
 차원 처리 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
