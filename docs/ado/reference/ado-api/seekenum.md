---
title: SeekEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7135d6582ea6d09c6f1b0ab3842c69d3d60d4fc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711419"
---
# <a name="seekenum"></a>SeekEnum
유형을 지정 [Seek](../../../ado/reference/ado-api/seek-method.md) 실행 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|같은 첫 번째 키를 찾고 *KeyValues*합니다.|  
|**adSeekLastEQ**|2|마지막 키 같음 검색 *KeyValues*합니다.|  
|**adSeekAfterEQ**|4|키 같음 검색 *KeyValues* 또는 일치 하는 발생 한 위치는 직후입니다.|  
|**adSeekAfter**|8|키 위치 바로 뒤에 검색 일치 하는 *KeyValues* 발생 합니다.|  
|**adSeekBeforeEQ**|16|키 같음 검색 *KeyValues*또는 일치 하는 발생 한 위치는 직전입니다.|  
|**adSeekBefore**|32|일치 하는 경우 키를 직전 seek *KeyValues* 발생 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
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
