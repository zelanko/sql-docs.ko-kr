---
title: 직접 실행 모드 | Microsoft Docs
description: LockType 속성이 adLockOptimistic 또는 Adlockoptimistic으로 설정 된 경우 적용 되는 즉시 실행 모드에 대해 설명 합니다.
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: rothja
ms.author: jroth
ms.openlocfilehash: e57d39fedb6509663ec21f28341d6bbca57dbd5c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980504"
---
# <a name="immediate-mode"></a>직접 실행 모드
직접 실행 모드는 **LockType** 속성이 **adlockoptimistic** 또는 **adlockoptimistic**으로 설정 된 경우에 적용 됩니다. 즉시 실행 모드에서는 **Update** 메서드를 호출 하 여 완료 된 행에 대해 작업을 선언 하는 즉시 레코드에 대 한 변경 내용이 데이터 소스에 전파 됩니다.  
  
## <a name="calling-update"></a>업데이트 호출  
 **Update** 메서드를 호출 하기 전에 추가 하거나 편집 하는 레코드에서 이동 하는 경우 ADO는 자동으로 **업데이트** 를 호출 하 여 변경 내용을 저장 합니다. 현재 레코드에 대 한 변경 내용을 취소 하거나 새로 추가 된 레코드를 삭제 하려면 탐색 전에 **CancelUpdate** 메서드를 호출 해야 합니다.  
  
 **Update** 메서드를 호출한 후에는 현재 레코드가 최신 상태로 유지 됩니다.  
  
## <a name="cancelupdate"></a>CancelUpdate  
 **CancelUpdate** 메서드를 사용 하 여 현재 행에 대 한 변경 내용을 취소 하거나 새로 추가 된 행을 삭제할 수 있습니다. 업데이트 메서드를 호출한 후에는 **업데이트** 메서드를 호출한 후 현재 행 또는 새 행에 대 한 변경 내용을 취소할 수 없습니다. 단, **RollbackTrans** 메서드 또는 일괄 처리 업데이트의 일부로 롤백할 수 있는 트랜잭션의 일부가 아닌 경우에 한 합니다. 일괄 처리 업데이트의 경우 **CancelUpdate** 또는 **CancelBatch** 메서드를 사용 하 여 **업데이트** 를 취소할 수 있습니다.  
  
 **CancelUpdate** 메서드를 호출할 때 새 행을 추가 하는 경우 현재 행은 **AddNew** 호출 이전의 현재 행이 됩니다.  
  
 현재 행을 변경 하거나 새 행을 추가 하지 않은 경우에는 **CancelUpdate** 메서드를 호출 하 여 오류를 생성 합니다.
