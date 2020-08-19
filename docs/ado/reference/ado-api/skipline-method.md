---
description: SkipLine 메서드
title: SkipLine 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: rothja
ms.author: jroth
ms.openlocfilehash: 463de3740ce29b859732c5ddb7ba69d58069f93f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442104"
---
# <a name="skipline-method"></a>SkipLine 메서드
텍스트 [스트림을](../../../ado/reference/ado-api/stream-object-ado.md)읽을 때 한 줄 전체를 건너뜁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>설명  
 다음 줄 구분 기호를 포함 하 여 모든 문자를 건너뜁니다. 기본적으로 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 는 **adcrlf**입니다. [Eos](../../../ado/reference/ado-api/eos-property.md)를 지나서 건너뛰려면 현재 위치가 **eos**에 유지 됩니다.  
  
 **SkipLine** 메서드는 텍스트 스트림과 함께 사용 됩니다 ([Type](../../../ado/reference/ado-api/type-property-ado-stream.md) is **adTypeText**).  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
