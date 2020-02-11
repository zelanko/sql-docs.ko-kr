---
title: 잠금 유형 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923804"
---
# <a name="types-of-locks"></a>잠금 형식
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 낙관적 일괄 처리 업데이트를 나타냅니다. 일괄 업데이트 모드에 필요 합니다.  
  
 많은 응용 프로그램에서 한 번에 여러 행을 인출 하 고, 삽입, 업데이트 또는 삭제 되는 전체 행 집합을 포함 하는 조정 된 업데이트를 수행 해야 합니다. 일괄 처리 커서를 사용 하는 경우 서버에 대 한 왕복만 필요 하므로 업데이트 성능이 향상 되 고 네트워크 트래픽이 감소 합니다. 일괄 처리 커서 라이브러리를 사용 하 여 정적 커서를 만든 다음 데이터 원본에서 연결을 끊을 수 있습니다. 이 시점에서 행을 변경한 후 다시 연결 하 여 일괄 처리의 데이터 원본에 변경 내용을 게시할 수 있습니다.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 **업데이트** 메서드를 호출할 때만 공급자에서 낙관적 잠금 잠금 레코드를 사용 함을 나타냅니다. 즉, 레코드를 편집 하는 시간과 **Update**를 호출 하는 시간 사이에 다른 사용자가 데이터를 변경할 수 있으며이로 인해 충돌이 발생 합니다. 충돌 가능성이 낮거나 충돌을 쉽게 해결할 수 있는 경우이 잠금 유형을 사용 합니다.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 비관적 잠금, 레코드 별로 기록 함을 나타냅니다. 공급자는 일반적으로 편집 전에 데이터 원본에서 레코드를 잠가 레코드를 성공적으로 편집할 수 있도록 하는 데 필요한 작업을 수행 합니다. 물론이는 업데이트를 호출 하 여 잠금을 해제할 때까지 다른 사용자가 편집을 시작한 후에는 레코드를 사용할 수 없음을 의미 합니다 **.** 예약 시스템에서와 같이 데이터를 동시에 변경 하는 것을 감당할 수 없는 시스템에서이 잠금 유형을 사용 합니다.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 읽기 전용 레코드를 나타냅니다. 데이터를 변경할 수 없습니다. 읽기 전용 잠금은 서버에서 레코드에 대 한 잠금을 유지 하지 않아도 되기 때문에 "가장 빠른" 유형입니다.  
  
## <a name="adlockunspecified"></a>adLockUnspecified 되지 않음  
 가 잠금 유형을 지정 하지 않습니다.
