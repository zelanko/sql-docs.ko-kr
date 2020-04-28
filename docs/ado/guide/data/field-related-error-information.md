---
title: 필드 관련 오류 정보 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7094c2dba004e35593f5ab11b1162efbdf3283c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925318"
---
# <a name="field-related-error-information"></a>필드 관련 오류 정보
오류가 필드와 직접 관련 된 경우, 예를 들어 데이터가 누락 된 경우 또는 필드의 형식이 잘못 된 경우에는 **필드** 개체의 **상태** 속성을 검사 하 여 문제의 원인에 대 한 자세한 정보를 검색할 수 있습니다. 이 속성은 문제에 대 한 특정 정보를 제공 하도록 향상 되었습니다. 예를 들어, 예를 들어, **UpdateBatch** 에 대 한 호출이 실패 하면 영향을 받는 각 레코드의 **필드** **상태** 속성을 검사 하 여 문제의 원인을 확인할 수 있습니다. 속성은 **Fieldstatusenum** 상수의 값 중 하나를 포함 합니다. 다음 표에는 오류가 발생할 때 특히 관심이 있는 값이 나와 있습니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|필드를 데이터 손실 없이 검색 하거나 저장할 수 없음을 나타냅니다.|  
|**adFieldDataOverflow**|6|공급자에서 반환 된 데이터가 필드의 데이터 형식을 오버플로 했음을 나타냅니다.|  
|**adFieldDefault**|13|필드의 기본값이 데이터를 설정할 때 사용 되었음을 나타냅니다.|  
|**adFieldIgnore**|15|원본에서 데이터 값을 설정할 때이 필드를 생략 했음을 나타냅니다. 공급자에 의해 값이 설정 되지 않았습니다.|  
|**adFieldIntegrityViolation**|10|필드가 계산 된 엔터티 또는 파생 된 엔터티 이므로 수정할 수 없음을 나타냅니다.|  
|**adFieldIsNull**|3|공급자에서 null 값을 반환 했음을 나타냅니다.|  
|**adFieldOutOfSpace**|22|공급자가 이동 또는 복사 작업을 완료 하기에 충분 한 저장소 공간을 확보할 수 없음을 나타냅니다.|
