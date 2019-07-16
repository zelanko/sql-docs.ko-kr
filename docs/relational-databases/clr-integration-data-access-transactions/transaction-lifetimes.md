---
title: 트랜잭션 수명 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
author: rothja
ms.author: jroth
ms.openlocfilehash: 759af22d445bb3c67db1f39ecf69dbeee1b666fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902484"
---
# <a name="transaction-lifetimes"></a>트랜잭션 수명
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 시작된 트랜잭션과 관리 코드에서 시작된 트랜잭션 사이에는 중요한 차이점이 있습니다. 즉, CLR(공용 언어 런타임) 코드에서는 CLR 호출 시작 또는 종료 시 불균형한 트랜잭션 상태를 허용하지 않습니다. 이 차이점으로 인해 발생하는 다음과 같은 문제점에 주의하십시오.  
  
-   CLR 프레임에서 시작된 트랜잭션을 커밋하거나 롤백하지 않으면 프레임 종료 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 오류를 생성합니다.  
  
-   외부 트랜잭션은 CLR 코드 내에서 커밋하거나 롤백할 수 없습니다.  
  
-   다른 프로시저에서 시작된 트랜잭션을 커밋하려고 하면 런타임 오류가 발생합니다.  
  
-   다른 프로시저에서 시작된 트랜잭션을 롤백하려고 하면 트랜잭션이 중단되어 다른 파생 작업이 수행되지 않습니다. 트랜잭션은 CLR 코드가 범위를 벗어날 때까지 중단됩니다. 프로시저 내에 오류가 있어 전체 트랜잭션을 종료하려는 경우에는 이 동작이 유용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 통합 및 트랜잭션](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
