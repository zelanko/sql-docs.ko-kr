---
title: 동적 커서 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab212d978f38a9e80435d0fae81a6664a8839b56
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270412"
---
# <a name="dynamic-cursors"></a>동적 커서
동적 커서는 커서 내부 또는 커서 외부의 다른 사용자가 변경 내용을에서 발생 하는지 여부에 관계 없이 결과 집합의 행에 대 한 모든 변경 내용을 검색 합니다. Insert, update 및 delete 문은 모든 사용자가 수행한 모든 커서를 통해 표시 됩니다. 동적 커서는 변경 내용이 행, 순서 및 커서가 열린 후에 결과 집합의 값을 검색할 수 있습니다. 커밋될 때까지 (아닌 경우 커서 트랜잭션 격리 수준을 "커밋되지 않은"로 설정 됨)에 업데이트 커서 밖에 서 표시 되지 않습니다.  
  
 예를 들어 동적 커서 인출 두 개의 행과 다른 응용 프로그램을 다음 행 중 하나를 업데이트 하 고 다른 삭제 합니다. 동적 커서는 행을 인출 합니다, 삭제 된 행을 검색 하지 않습니다 이지만 업데이트 된 행에 대 한 새 값이 표시 됩니다.  
  
 동적 커서는 응용 프로그램에서 다른 사용자가 수행한 모든 동시 업데이트를 검색 해야 하는 경우 좋은 선택 합니다. 사용 하 여는 **adOpenDynamic CursorTypeEnum** ADO에서 동적 커서를 사용 해야 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [정적 커서](../../../ado/guide/data/static-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)
