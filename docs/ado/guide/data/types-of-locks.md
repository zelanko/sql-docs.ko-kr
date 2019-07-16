---
title: 잠금의 종류 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93436a5180f1a01269f1612f7e608b71b4c073e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923804"
---
# <a name="types-of-locks"></a>잠금 형식
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 낙관적 일괄 처리 업데이트를 나타냅니다. 일괄 업데이트 모드에 필요합니다.  
  
 많은 응용 프로그램이 한 번에 많은 행을 인출 하 고 삽입, 업데이트 또는 삭제 된 행의 전체 집합을 포함 하는 조정 된 업데이트를 확인 해야 합니다. 서버로 왕복 이동 필요한 하나의 일괄 처리 커서를 사용 하 여 되므로 업데이트 성능이 향상 되 고 네트워크 트래픽이 줄어듭니다. Batch 커서 라이브러리를 사용 하는 정적 커서를 만들 수 있으며 데이터 원본의 다음 연결을 끊을 수도 있습니다. 이 시점에서 수 변경 행 및 이후에 다시 연결 하 고 일괄 처리의 데이터 원본에 변경 내용을 게시 합니다.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 공급자는 낙관적 잠금-레코드를 호출 하는 경우에 잠금 나타냅니다 합니다 **업데이트** 메서드. 레코드를 호출 하는 경우 편집이 즉, 다른 사용자가 시간 간에 데이터를 변경할 수 있습니다 수 있는지 **업데이트**, 충돌 만듭니다. 충돌 가능성이 낮은 상황에서이 잠금 유형을 사용 하거나 충돌 쉽게 해결할 수 있습니다.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 비관적 잠금, 레코드를 나타냅니다. 공급자가 잠금 레코드 편집 하기 전에 즉시 데이터 원본에 일반적으로 레코드를 제대로 편집 하는 데 필요한 합니다. 물론, 즉는 레코드를 사용할 수 없는 다른 사용자에 게 호출 하 여 잠금을 해제할 때까지 편집을 시작한 경우 **업데이트 합니다.** 와 같은 데이터에 대 한 동시 변경을 예약 시스템에 있는 중지할 수 없는 시스템에서 이러한 유형의 잠금을 사용 합니다.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 읽기 전용으로 레코드를 나타냅니다. 데이터를 변경할 수 없습니다. 읽기 전용 잠금을 "가장 빠른" 유형의 잠금 이므로 레코드에 대 한 잠금을 유지 하기 위해 서버 필요 하지 않습니다.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 잠금의 종류를 지정 하지 않습니다.
