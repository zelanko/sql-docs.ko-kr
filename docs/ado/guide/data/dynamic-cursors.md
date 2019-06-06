---
title: 동적 커서 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b2fe669c521e1d21b46b6eb503f0ca03944e12e9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702080"
---
# <a name="dynamic-cursors"></a>동적 커서
동적 커서는 커서 내에서 또는 커서 외부의 다른 사용자가 변경에서 발생 하는지 여부에 관계 없이 결과 집합의 행에 대 한 모든 변경 내용을 검색 합니다. Insert, update 및 delete 문은 모든 사용자가 수행한 모든 커서를 통해 표시 됩니다. 동적 커서 행, 순서 및 결과 집합 커서가 열린 후에 값에 대 한 변경 내용을 감지할 수 있습니다. (커서 트랜잭션 격리 수준이 설정 되지 않았으면 "커밋되지 않은") 커밋될 때까지 업데이트 커서 밖에 서 표시 되지 않습니다.  
  
 예를 들어 동적 커서 두 개의 행과 다른 응용 프로그램을 가져오는 다음 이러한 행 중 하나를 업데이트 하 고 다른 삭제 합니다. 그런 다음, 동적 커서가 해당 행을 페치하는 경우, 삭제된 행을 찾을 수 없지만 업데이트된 행에 대한 새 값을 표시합니다.  
  
 동적 커서는 적합 한 경우 응용 프로그램에서 다른 사용자가 변경한 모든 동시 업데이트를 검색 해야 합니다. 사용 하 여는 **adOpenDynamic CursorTypeEnum** ado에서 동적 커서를 사용 해야 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [정적 커서](../../../ado/guide/data/static-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)
