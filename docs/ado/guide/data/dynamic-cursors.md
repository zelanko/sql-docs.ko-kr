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
ms.openlocfilehash: 86e51b7880004117e8efc96bd310c6de705d43a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925504"
---
# <a name="dynamic-cursors"></a>동적 커서
동적 커서는 변경 내용이 커서 내부에서 발생 하는지 아니면 커서 외부의 다른 사용자에 의해 변경 되는지에 관계 없이 결과 집합의 행에 대 한 모든 변경 내용을 검색 합니다. 모든 사용자가 수행한 모든 insert, update 및 delete 문은 커서를 통해 볼 수 있습니다. 동적 커서는 커서를 연 후 결과 집합에서 행, 순서 및 값에 대 한 변경 내용을 검색할 수 있습니다. 커서 트랜잭션 격리 수준이 "커밋되지 않음"으로 설정 되지 않은 경우 커서 외부에서 수행 된 업데이트는 커밋될 때까지 표시 되지 않습니다.  
  
 예를 들어 동적 커서가 두 개의 행과 다른 응용 프로그램을 페치 한 다음 해당 행 중 하나를 업데이트 하 고 다른 응용 프로그램을 삭제 한다고 가정 합니다. 그런 다음, 동적 커서가 해당 행을 페치하는 경우, 삭제된 행을 찾을 수 없지만 업데이트된 행에 대한 새 값을 표시합니다.  
  
 응용 프로그램에서 다른 사용자가 수행한 모든 동시 업데이트를 검색 해야 하는 경우에는 동적 커서를 선택 하는 것이 좋습니다. **AdOpenDynamic CursorTypeEnum** 를 사용 하 여 ADO에서 동적 커서를 사용 하도록 지정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [앞 으로만 이동 가능한 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [정적 커서](../../../ado/guide/data/static-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)
