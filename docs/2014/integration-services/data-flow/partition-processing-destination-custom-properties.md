---
title: 파티션 처리 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dbab24f756498d7427f9961e4176249daac8dfb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770949"
---
# <a name="partition-processing-destination-custom-properties"></a>파티션 처리 대상 사용자 지정 속성
  파티션 처리 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 파티션 처리 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 대한 연결 문자열입니다.|  
|KeyDuplicate|Integer(열거형)|UseDefaultConfiguration가 인 `False`경우 중복 키 오류를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError`(0), `ReportAndContinue`(1) 및 `ReportAndStop`(2)입니다. 이 속성의 기본값은 `IgnoreError`(0)입니다.|  
|KeyErrorAction|Integer(열거형)|UseDefaultConfiguration가 인 `False`경우 키 오류를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `ConvertToUnknown`(0) 및 `DiscardRecord`(1)입니다. 이 속성의 기본값은 `ConvertToUnknown`(0)입니다.|  
|KeyErrorLimit|정수|UseDefaultConfiguration가 인 `False`경우 허용 되는 키 오류의 상한입니다.|  
|KeyErrorLimitAction|Integer(열거형)|UseDefaultConfiguration이 `False`인 경우에 도달할 때 `KeyErrorLimit` 수행할 동작을 나타내는 값입니다. 가능한 값은 `StopLogging`(1) 및 `StopProcessing`(0)입니다. 이 속성의 기본값은 `StopProcessing`(0)입니다.|  
|KeyErrorLogFile|String|UseDefaultConfiguration이 인 `False`경우 오류 로그 파일의 경로 및 파일 이름입니다.|  
|KeyNotFound|Integer(열거형)|UseDefaultConfiguration가 인 `False`경우 누락 된 키 오류를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError`(0), `ReportAndContinue`(1) 및 `ReportAndStop`(2)입니다. 이 속성의 기본값은 `ReportAndContinue`(1)입니다.|  
|NullKeyConvertedToUnknown|Integer(열거형)|UseDefaultConfiguration가 인 `False`경우 알 수 없는 값으로 변환 된 null 키를 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError`(0), `ReportAndContinue`(1) 및 `ReportAndStop`(2)입니다. 이 속성의 기본값은 `IgnoreError`(0)입니다.|  
|NullKeyNotAllowed|Integer(열거형)|UseDefaultConfiguration가 인 `False`경우 허용 되지 않는 null을 처리 하는 방법을 나타내는 값입니다. 가능한 값은 `IgnoreError`(0), `ReportAndContinue`(1) 및 `ReportAndStop`(2)입니다. 이 속성의 기본값은 `ReportAndContinue`(1)입니다.|  
|ProcessType|Integer(열거형)|변환에서 사용하는 파티션 처리의 유형입니다. 가능한 값은 `ProcessAdd`(1)(증분), `ProcessFull`(0) 및 `ProcessUpdate`(2)입니다.|  
|UseDefaultConfiguration|부울|변환에서 기본 오류 구성을 사용하는지 여부를 지정하는 값입니다. 이 속성이 인 `False`경우 변환은 Keyduplicate, KeyErrorAction 등을 비롯 하 여이 표에 나열 된 오류 처리 사용자 지정 속성의 값을 사용 합니다.|  
  
 파티션 처리 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Partition Processing Destination](partition-processing-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Common Properties](../common-properties.md)  
  
  
