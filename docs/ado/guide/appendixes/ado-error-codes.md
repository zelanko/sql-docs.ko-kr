---
description: ADO 오류 코드 캡처
title: ADO 오류 코드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: b5c3f5f00355bb2c9f9762db1d317a592b4df7dc
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805340"
---
# <a name="capture-ado-error-codes"></a>ADO 오류 코드 캡처
[오류 컬렉션의](../../reference/ado-api/errors-collection-ado.md) [오류](../../reference/ado-api/error-object.md) 개체에서 반환 되는 공급자 오류 외에도 ADO 자체에서 런타임 환경의 예외 처리 메커니즘에 대 한 오류를 반환할 수 있습니다. Microsoft® Visual Basic의 **On error** 문과 같이 프로그래밍 언어의 오류 트래핑 메커니즘을 사용 하거나 Microsoft Visual C++®의 **try-catch 블록을 사용 하 여 ADO** 오류를 캡처합니다.

 ADO 오류 코드 목록은 [Errorvalueenum](../../reference/ado-api/errorvalueenum.md)을 참조 하십시오.

## <a name="see-also"></a>참고 항목
 [오류 개체](../../reference/ado-api/error-object.md) [오류 수집 (ADO)](../../reference/ado-api/errors-collection-ado.md)