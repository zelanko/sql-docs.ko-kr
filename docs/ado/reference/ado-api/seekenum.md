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
ms.openlocfilehash: 886825b4d32354572a5162487add419b00ec35d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931064"
---
# <a name="seekenum"></a>SeekEnum
실행할 [검색](../../../ado/reference/ado-api/seek-method.md) 유형을 지정 합니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|*Keyvalues*와 동일한 첫 번째 키를 검색 합니다.|  
|**adSeekLastEQ**|2|*Keyvalues*와 동일한 마지막 키를 검색 합니다.|  
|**adSeekAfterEQ**|4|*Keyvalues* 와 동일한 키를 검색 하거나, 일치 하는 항목이 발생 한 후 바로 검색 합니다.|  
|**adSeekAfter**|8|*Keyvalues* 와 일치 하는 항목이 발생 한 후 바로 키를 검색 합니다.|  
|**adSeekBeforeEQ**|16|키가 *Keyvalues*와 같거나 그 바로 앞에 있는 키 중 하나를 검색 합니다.|  
|**adSeekBefore**|32|*Keyvalues* 와 일치 하는 항목이 발생 하는 위치 바로 앞에서 키를 검색 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|지속적임|  
|--------------|  
|AdoEnums. FIRSTEQ|  
|AdoEnums. LASTEQ|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. BEFOREEQ|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
 [Seek 메서드](../../../ado/reference/ado-api/seek-method.md)
