---
title: 트랜잭션 수명 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c56a98e5cd9670f8dd3a86265aa50a7f0f57b5af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181831"
---
# <a name="transaction-lifetimes"></a>트랜잭션 수명
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 시작된 트랜잭션과 관리 코드에서 시작된 트랜잭션 사이에는 중요한 차이점이 있습니다. 즉, CLR(공용 언어 런타임) 코드에서는 CLR 호출 시작 또는 종료 시 불균형한 트랜잭션 상태를 허용하지 않습니다. 이 차이점으로 인해 발생하는 다음과 같은 문제점에 주의하십시오.  
  
-   CLR 프레임에서 시작된 트랜잭션을 커밋하거나 롤백하지 않으면 프레임 종료 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 오류를 생성합니다.  
  
-   외부 트랜잭션은 CLR 코드 내에서 커밋하거나 롤백할 수 없습니다.  
  
-   다른 프로시저에서 시작된 트랜잭션을 커밋하려고 하면 런타임 오류가 발생합니다.  
  
-   다른 프로시저에서 시작된 트랜잭션을 롤백하려고 하면 트랜잭션이 중단되어 다른 파생 작업이 수행되지 않습니다. 트랜잭션은 CLR 코드가 범위를 벗어날 때까지 중단됩니다. 프로시저 내에 오류가 있어 전체 트랜잭션을 종료하려는 경우에는 이 동작이 유용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 통합 및 트랜잭션](../native-client-ole-db-transactions/transactions.md)  
  
  