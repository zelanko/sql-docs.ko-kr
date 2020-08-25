---
description: SeekEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e60bbc81f7b40dac7d1564a32f1e60eb8456c9bf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777502"
---
# <a name="seekenum"></a>SeekEnum
실행할 [검색](./seek-method.md) 유형을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|*Keyvalues*와 동일한 첫 번째 키를 검색 합니다.|  
|**adSeekLastEQ**|2|*Keyvalues*와 동일한 마지막 키를 검색 합니다.|  
|**adSeekAfterEQ**|4|*Keyvalues* 와 동일한 키를 검색 하거나, 일치 하는 항목이 발생 한 후 바로 검색 합니다.|  
|**adSeekAfter**|8|*Keyvalues* 와 일치 하는 항목이 발생 한 후 바로 키를 검색 합니다.|  
|**adSeekBeforeEQ**|16|키가 *Keyvalues*와 같거나 그 바로 앞에 있는 키 중 하나를 검색 합니다.|  
|**adSeekBefore**|32|*Keyvalues* 와 일치 하는 항목이 발생 하는 위치 바로 앞에서 키를 검색 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. FIRSTEQ|  
|AdoEnums. LASTEQ|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. BEFOREEQ|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
 [Seek 메서드](./seek-method.md)