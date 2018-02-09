---
title: "잠금의 종류 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9bec4523ea458998ff19481de467cc6493d03ed2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="types-of-locks"></a>잠금의 종류
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 낙관적 일괄 업데이트를 나타냅니다. 일괄 업데이트 모드에 필요합니다.  
  
 대부분의 응용 프로그램 행 수를 한 번에 인출 하 고 삽입, 업데이트 또는 삭제 된 행의 전체 집합을 포함 하는 조정 된 업데이트를 확인 해야 합니다. 서버에 왕복 필요 하나 일괄 커서를 사용 되므로 업데이트 성능이 향상 되 고 네트워크 트래픽이 줄어듭니다. 일괄 처리 커서 라이브러리를 사용 하 여 있습니다 정적 커서를 만들고 데이터 원본의 다음 연결을 끊을 수 있습니다. 이 시점에서 수 변경 행 및 이후에 다시 연결 하 고 일괄 처리에서 데이터 원본에 변경 내용을 게시 합니다.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 낙관적 잠금 공급자를 사용 함을 나타냅니다-레코드를 호출 하는 경우에 잠금는 **업데이트** 메서드. 레코드를 호출 하는 경우 편집이 즉, 다른 사용자는 시간 사이 데이터를 변경 될 수 있다는 가능성이 매우 **업데이트**, 충돌 만듭니다. 이 잠금 유형을 충돌 가능성이 모두 낮은 경우에 사용 하거나 충돌 쉽게 해결할 수 있습니다.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 레코드 별로 비관적 잠금을 나타냅니다. 공급자는는 제대로 잠금으로써 레코드 편집 하기 직전 데이터 원본에 일반적으로 여 레코드를 편집 하는 데 필요한 작업을 수행 합니다. 물론, 즉, 호출 하 여 잠금을 해제할 때까지 편집할을 시작한 경우 레코드 다른 사용자에 게 사용할 수 없는지 **업데이트 합니다.** 수 없는 예약 시스템에서와 같은 데이터 동시 변경 내용을 하도록 시스템에 이러한 유형의 잠금을 사용 합니다.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 읽기 전용 레코드를 나타냅니다. 데이터를 변경할 수 없습니다. 읽기 전용으로 잠겨 "빠른" 잠금 유형을 레코드에 대 한 잠금을 유지 하기 위해 서버는 필요 하지 않기 때문에 있습니다.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 잠금 유형을 지정 하지 않습니다.
