---
description: ResyncEnum
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: rothja
ms.author: jroth
ms.openlocfilehash: addaaa07b14b88ed7d72714ba8698da1f2ef2ac9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777642"
---
# <a name="resyncenum"></a>ResyncEnum
다시 [동기화](./resync-method.md)를 호출 하 여 기본 값을 덮어쓸지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|기본값 데이터를 덮어쓰고 보류 중인 업데이트가 취소 됩니다.|  
|**adResyncUnderlyingValues**|1|는 데이터를 덮어쓰지 않으며 보류 중인 업데이트는 취소 되지 않습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums. UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>적용 대상  
 [Resync 메서드](./resync-method.md)