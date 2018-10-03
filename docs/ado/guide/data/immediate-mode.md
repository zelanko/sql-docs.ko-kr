---
title: 직접 실행 모드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ff8782287f5a6cbeb3f22ca58eaa3bd061c6c89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657671"
---
# <a name="immediate-mode"></a>직접 실행 모드
직접 실행 모드에 적용 되는 경우는 **LockType** 속성이 **adLockOptimistic** 또는 **adLockPessimistic**합니다. 직접 실행 모드에서 레코드를 변경할은 데이터 원본에 즉시 전파를 호출 하 여 행에 대 한 작업 완료를 선언 합니다 **업데이트** 메서드.  
  
## <a name="calling-update"></a>업데이트를 호출합니다.  
 레코드에서 이동 하는 경우 추가 또는 편집 하는 호출 하기 전에 합니다 **업데이트** 메서드를 ADO를 자동으로 호출 **업데이트** 변경 내용을 저장 합니다. 호출 해야 합니다 **CancelUpdate** 메서드를 탐색 하려면 현재 레코드에 변경한 내용을 취소 하거나 새로 추가 된 레코드를 삭제 하기 전에 합니다.  
  
 현재 레코드를 호출한 후 계속 합니다 **업데이트** 메서드.  
  
## <a name="cancelupdate"></a>CancelUpdate  
 사용 된 **CancelUpdate** 메서드를 현재 행에 대 한 변경 내용을 취소 하거나 새로 추가 된 행을 삭제 합니다. 호출한 후 새 행을 현재 행에 변경 내용을 취소할 수 없습니다는 **업데이트** 메서드를 변경 내용을 사용 하 여 롤백할 수 있는 트랜잭션의 일부인 경우가 아니면 합니다 **RollbackTrans** 의 일부나 메서드 일괄 업데이트 합니다. 일괄 업데이트의 경우 취소할 수 있습니다 합니다 **업데이트** 사용 하 여 합니다 **CancelUpdate** 또는 **CancelBatch** 메서드.  
  
 호출 하는 경우 새 행을 추가 하는 경우는 **CancelUpdate** 메서드를 현재 행이 행 하기 전에 현재 합니다 **AddNew** 호출 합니다.  
  
 현재 행을 변경 하지 않았거나 새 행을 추가 하는 경우 호출 된 **CancelUpdate** 메서드는 오류를 생성 합니다.
