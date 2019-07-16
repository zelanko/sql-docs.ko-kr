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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925318"
---
# <a name="field-related-error-information"></a>필드 관련 오류 정보
경우는 오류는 필드에 직접 연관 됩니다 예를 들어, 데이터를 사용할 수 없는 경우 또는-필드에 대 한 잘못 된 경우 검색할 수 있습니다 문제의 원인에 대 한 자세한 내용은 검사 하 여 합니다 **필드** 개체의 **상태**  속성입니다. 이 속성 문제에 대 한 특정 정보를 제공 하도록 향상 되었습니다. 따라서 예를 들어 호출 하 여 **UpdateBatch** 실패 하면 문제의 원인을 검사 하 여 확인할 수 있습니다 합니다 **상태** 속성을 **필드** 는 영향을 받는 각 기록 합니다. 속성의 값 중 하나가 포함 됩니다는 **FieldStatusEnum** 상수입니다. 다음 표에서 관심 있는 특정 오류가 발생 하면 해당 값을 포함 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|필드 검색 하거나 데이터의 손실 없이 저장할 수 없습니다 나타냅니다.|  
|**adFieldDataOverflow**|6|공급자에서 반환 되는 데이터 필드의 데이터 형식을 오버플로 나타냅니다.|  
|**adFieldDefault**|13|데이터를 설정 하는 경우 필드에 대 한 기본값을 사용 했는지를 나타냅니다.|  
|**adFieldIgnore**|15|설정 데이터 소스의 값이 될 때이 필드를 건너뜀을 나타냅니다. 값은 공급자가 설정 되었습니다.|  
|**adFieldIntegrityViolation**|10|계산 또는 파생 엔터티 이기 때문에 필드를 수정할 수 없습니다 나타냅니다.|  
|**adFieldIsNull**|3|공급자는 null 값을 반환 했음을 나타냅니다.|  
|**adFieldOutOfSpace**|22|공급자는 이동 작업을 완료 또는 복사 작업에 충분 한 저장소 공간을 획득할 수 임을 나타냅니다.|
