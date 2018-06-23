---
title: 차원 처리 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f4dae4c9661e8a04e34b5d2b78ccdd0f556bfa7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079813"
---
# <a name="dimension-processing-destination-custom-properies"></a>차원 처리 대상 사용자 지정 속성
  차원 처리 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 차원 처리 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 연결 문자열입니다.|  
|KeyDuplicate|Integer(열거형)|UseDefaultConfiguration 다음과 같은 경우 `False`, 중복 키 오류를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError` (0), `ReportAndContinue` (1) 및 `ReportAndStop` (2). 이 속성의 기본값은 `IgnoreError` (0).|  
|KeyErrorAction|Integer(열거형)|UseDefaultConfiguration 다음과 같은 경우 `False`, 키 오류를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `ConvertToUnknown`(0) 및 `DiscardRecord`(1)입니다. 이 속성의 기본값은 `ConvertToUnknown` (0).|  
|KeyErrorLimit|정수|UseDefaultConfiguration 다음과 같은 경우 `False`, 사용 하도록 설정 된 키 오류의 상한값입니다.|  
|KeyErrorLimitAction|Integer(열거형)|UseDefaultConfiguration 다음과 같은 경우 `False`때 수행할 동작을 지정 하는 값 `KeyErrorLimit` 에 도달 합니다. 가능한 값은 `StopLogging`(1) 및 `StopProcessing`(0)입니다. 이 속성의 기본값은 `StopProcessing` (0).|  
|KeyErrorLogFile|String|UseDefaultConfiguration 다음과 같은 경우 `False`, 오류 로그 파일의 경로 파일 이름입니다.|  
|KeyNotFound|Integer(열거형)|UseDefaultConfiguration 다음과 같은 경우 `False`, 키 누락 오류를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError` (0), `ReportAndContinue` (1) 및 `ReportAndStop` (2). 이 속성의 기본값은 `IgnoreError` (0).|  
|NullKeyConvertedToUnknown|Integer(열거형)|UseDefaultConfiguration 다음과 같은 경우 `False`, 알 수 없는 값으로 변환 된 null 키를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError` (0), `ReportAndContinue` (1) 및 `ReportAndStop` (2). 이 속성의 기본값은 `IgnoreError` (0).|  
|NullKeyNotAllowed|Integer(열거형)|UseDefaultConfiguration 다음과 같은 경우 `False`, 허용 되지 않는 null을 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError` (0), `ReportAndContinue` (1) 및 `ReportAndStop` (2). 이 속성의 기본값은 `IgnoreError` (0).|  
|ProcessType|Integer(열거형)|변환에서 사용하는 차원 처리의 유형입니다. 값은 `ProcessAdd`(1)(증분), `ProcessFull`(0) 및 `ProcessUpdate`(2)입니다.|  
|UseDefaultConfiguration|Boolean|변환에서 기본 오류 구성을 사용하는지 여부를 지정하는 값입니다. 이 속성이 `False`, 변환에는 오류 처리에 대 한 정보가 포함 됩니다.|  
  
 차원 처리 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Dimension Processing Destination](dimension-processing-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Common Properties](../common-properties.md)  
  
  