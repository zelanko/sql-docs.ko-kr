---
title: SkipLine 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac4551bfe1859e49cfd88326b1223cbac3fc9a23
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="skipline-method"></a>SkipLine 메서드
텍스트를 읽을 때 한 줄 전체를 건너뜁니다 [스트림](../../../ado/reference/ado-api/stream-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>주의  
 및 다음 선 구분 기호가까지 모든 문자는 무시 됩니다. 기본적으로는 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 은 **adCRLF**합니다. 지난 건너뛸 하려고 하면 [EOS](../../../ado/reference/ado-api/eos-property.md), 현재 위치에 유지 됩니다 **EOS**합니다.  
  
 **SkipLine** 메서드 텍스트 스트림 함께 사용 됩니다 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 은 **adTypeText**).  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
