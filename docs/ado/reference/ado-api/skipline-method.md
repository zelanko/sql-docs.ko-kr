---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0e96900fdac55e97e3481ba5198e0f51d659877
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713761"
---
# <a name="skipline-method"></a>SkipLine 메서드
텍스트를 읽을 때 줄 전체를 건너뜁니다 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Remarks  
 다음 줄 구분 기호를 포함 하는 모든 문자는 무시 됩니다. 기본적으로 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 됩니다 **adCRLF**합니다. 건너뛰어야 하려고 [EOS](../../../ado/reference/ado-api/eos-property.md), 현재 위치가 유지 됩니다 **EOS**합니다.  
  
 **SkipLine** 메서드는 텍스트 스트림 사용 됩니다 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 는 **adTypeText**).  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
