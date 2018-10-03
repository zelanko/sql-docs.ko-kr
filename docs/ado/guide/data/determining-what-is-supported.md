---
title: 지원 되는 확인 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 835584da4c51f5e65306d0609b4e69f78a7d58b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707571"
---
# <a name="determining-what-is-supported"></a>지원되는 기능 확인
합니다 **지원** 메서드는 지정 된 확인 데 **레코드 집합** 개체는 특정 종류의 기능을 지원 합니다. 다음 구문이 사용:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Remarks  
 합니다 **지원** 메서드 공급자의 모든 CursorOptions 인수에 의해 식별 된 기능을 지원 하는지 여부를 나타내는 부울 값을 반환 합니다. 사용할 수는 **지원** 기능의 유형을 확인 하는 방법을 **레코드 집합** 지원 개체입니다. 경우는 **레코드 집합** 개체에 있는 해당 상수는 기능을 지원 합니다 *CursorOptions*의 **지 원하는** 메서드가 반환 되는 **True**. 그렇지 **False**합니다.  
  
 사용 하 여는 **지원** 메서드의 기능에 대 한 확인할 수 있습니다 합니다 **레코드 집합** 책갈피를 사용 하 여 새 레코드를 추가, 사용 하 여 개체를 **찾을** 메서드를 사용 하 여 스크롤을 사용 합니다  **인덱스** 속성 및 일괄 처리 업데이트를 수행 합니다. 상수 및 해당 의미의 전체 목록은 참조 하세요 [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)합니다.  
  
 하지만 합니다 **지원** 메서드를 반환할 수 있습니다 **True** 지정된 된 기능에 대 한 보장 하지는 않습니다 공급자를 사용할 수 있는 기능을 모든 상황입니다. 합니다 **지원** 메서드는 단순히 특정 조건이 충족 될 된다는 가정 하는 공급자 지정 된 기능을 지원할 수 있는지 여부를 반환 합니다. 예를 들어, 합니다 **지원** 메서드 되었음을 나타낼 수는 **레코드 집합** 커서 여러 개의 테이블 조인을 기반으로 하는 경우에 개체에 업데이트를 지원-는 일부 열은 업데이트할 수 없습니다.
