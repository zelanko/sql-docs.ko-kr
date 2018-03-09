---
title: "직접 실행 모드 | Microsoft Docs"
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
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f737d3b05e27eff7aae0aa95ee336a054c38f29f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="immediate-mode"></a>직접 실행 모드
직접 실행 모드 적용 되는 경우는 **LockType** 속성이로 설정 되어 **adLockOptimistic** 또는 **adLockPessimistic**합니다. 직접 실행 모드에서 변경 내용이 레코드에 전파 되는 데이터 소스에 호출 하 여 행에 대 한 작업 완료를 선언 하는 즉시는 **업데이트** 메서드.  
  
## <a name="calling-update"></a>업데이트를 호출합니다.  
 레코드에서 이동 하는 경우 추가 하거나 편집 하는 호출 하기 전에 **업데이트** 메서드, ADO를 자동으로 호출 **업데이트** 여 변경 내용을 저장 합니다. 호출 해야 합니다는 **CancelUpdate** 현재 레코드에 변경한 내용을 취소 하거나 새로 추가 된 레코드를 삭제 하려는 경우 이동 하기 전에 메서드.  
  
 호출한 후에 현재 레코드가 남아는 **업데이트** 메서드.  
  
## <a name="cancelupdate"></a>CancelUpdate  
 사용 하 여는 **CancelUpdate** 메서드를 현재 행에 대해 변경 내용을 취소 하거나 새로 추가 된 행을 삭제 합니다. 호출한 후 현재 행 또는 새 행 변경 내용을 취소할 수 없습니다는 **업데이트** 메서드를 변경으로 롤백할 수 있는 트랜잭션의 일부인 경우가 아니면는 **RollbackTrans** 의 일부나 메서드 일괄 업데이트 합니다. 일괄 처리 업데이트의 경우 취소할 수 있습니다는 **업데이트** 와 **CancelUpdate** 또는 **CancelBatch** 메서드.  
  
 호출 하는 경우 새 행 추가 하는 경우는 **CancelUpdate** 메서드를 현재 행이 이전의 현재 행에서 **AddNew** 호출 합니다.  
  
 현재 행을 변경 하거나 새 행을 추가 하지, 하는 경우 호출 된 **CancelUpdate** 오류가 발생 합니다.
