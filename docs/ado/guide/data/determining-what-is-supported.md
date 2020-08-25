---
description: 지원되는 기능 확인
title: 지원 되는 항목 확인 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: rothja
ms.author: jroth
ms.openlocfilehash: 769004bd74b248188cfa96e633ce5961d2330838
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806902"
---
# <a name="determining-what-is-supported"></a>지원되는 기능 확인
**Supports** 메서드는 지정 된 **레코드 집합** 개체가 특정 유형의 기능을 지원 하는지 여부를 확인 하는 데 사용 됩니다. 다음 구문이 있습니다.  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>설명  
 **Supports** 메서드는 공급자가 CursorOptions 인수에 의해 식별 되는 모든 기능을 지원 하는지 여부를 나타내는 부울 값을 반환 합니다. **Supports** 메서드를 사용 하 여 **레코드 집합** 개체가 지 원하는 기능 유형을 확인할 수 있습니다. **Recordset** 개체가 *CursorOptions*에 있는 해당 상수를 포함 하는 기능을 지 원하는 경우 **지원** 메서드는 **True**를 반환 합니다. 그렇지 않으면 **False**를 반환 합니다.  
  
 **지원** 메서드를 사용 하 여 **레코드 집합** 개체가 새 레코드를 추가 하 고, 책갈피를 사용 하 고, **찾기** 메서드를 사용 하 고, 스크롤을 사용 하 고, **인덱스** 속성을 사용 하 고, 일괄 업데이트를 수행할 수 있는지 확인할 수 있습니다. 상수 및 해당 의미의 전체 목록은 [CursorOptionEnum](../../reference/ado-api/cursoroptionenum.md)를 참조 하세요.  
  
 **지원** 메서드는 지정 된 기능에 대해 **True** 를 반환할 수 있지만, 공급자가 모든 상황에서 기능을 사용할 수 있도록 보장 하지는 않습니다. **Supports** 메서드는 특정 조건이 충족 될 경우 공급자가 지정 된 기능을 지원할 수 있는지 여부를 반환 합니다. 예를 들어 **지원** 메서드는 커서가 여러 테이블 조인에 기반 하 고 있지만 업데이트할 수 없는 일부 열을 기반으로 하더라도 **Recordset** 개체가 업데이트를 지원함을 나타낼 수 있습니다.