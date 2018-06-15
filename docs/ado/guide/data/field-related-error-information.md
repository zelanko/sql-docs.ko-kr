---
title: 필드와 관련 된 오류 정보 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0ae8e1717300b88650eb67225ff69b107efc5dc
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270112"
---
# <a name="field-related-error-information"></a>필드와 관련 된 오류 정보
필드와 관련이 직접 오류가 발생 하는 경우-예를 들어 데이터가 누락 되어 또는 필드에 대 한 잘못 된 형식이 된 경우-검사 하 여 문제의 원인에 대 한 자세한 정보를 검색할 수 있습니다는 **필드** 개체의 **상태**  속성입니다. 이 속성의 문제에 대 한 특정 정보를 제공 하도록 향상 되었습니다. 따라서, 예를 들어를 호출할 때 **UpdateBatch** 실패 하면 문제의 원인을 검토 하 여 확인할 수 있습니다는 **상태** 의 속성은 **필드** 는 영향을 받는 각 레코드가 있습니다. 속성의 값 중 하나가 포함 됩니다는 **FieldStatusEnum** 상수입니다. 다음 표에서 오류가 발생 한 경우 특정 관심 있는 해당 값을 포함 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|필드 검색 하거나 데이터의 손실 없이 저장할 수 없습니다 나타냅니다.|  
|**adFieldDataOverflow**|6|공급자에서 반환 되는 데이터 필드의 데이터 형식을 오버플로 있는지를 나타냅니다.|  
|**adFieldDefault**|13|데이터를 설정할 때 필드에 대 한 기본값 사용 되었음을 나타냅니다.|  
|**adFieldIgnore**|15|설정 데이터 소스에 값이 될 때이 필드를 건너뛰었음을 나타냅니다. 공급자가 없는 값이 설정 됩니다.|  
|**adFieldIntegrityViolation**|10|필드는 계산 된 또는 파생 된 엔터티 이기 때문에 수정 될 수 없음을 나타냅니다.|  
|**adFieldIsNull**|3|공급자는 null 값을 반환 했음을 나타냅니다.|  
|**adFieldOutOfSpace**|22|공급자가 충분 한 저장 공간 완료 이동 또는 복사 작업을 가져올 수 있는지를 나타냅니다.|
