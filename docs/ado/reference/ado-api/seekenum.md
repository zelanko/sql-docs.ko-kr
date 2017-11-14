---
title: SeekEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 051f4e1c300796e2777e9b06a1514c9ce00b9b02
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="seekenum"></a>SeekEnum
유형을 지정 [Seek](../../../ado/reference/ado-api/seek-method.md) 실행할 수 있습니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1.|같은 첫 번째 키를 찾고 *KeyValues*합니다.|  
|**adSeekLastEQ**|2|검색 (seek)의 마지막 키와 같지 *KeyValues*합니다.|  
|**adSeekAfterEQ**|4|같은 중 하나는 키를 찾고 *KeyValues* 위나 바로 뒤와 일치 하는 었어야 합니다.|  
|**adSeekAfter**|8|키를 where 직후 검색 (seek) 일치 하는 *KeyValues* 발생 합니다.|  
|**adSeekBeforeEQ**|16|같은 중 하나는 키 검색 (seek) *KeyValues*또는 바로 앞과 일치 하는 었어야 합니다.|  
|**adSeekBefore**|32|일치 하는 경우 키 바로 앞 seek *KeyValues* 발생 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>적용 대상  
 [Seek 메서드](../../../ado/reference/ado-api/seek-method.md)

