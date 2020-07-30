---
title: sys. sp_rda_reconcile_indexes (Transact-sql) | Microsoft Docs
description: Sp_rda_reconcile_indexes에 대해 자세히 알아보세요. 이 Transact-sql 저장 프로시저를 사용 하 여 스키마 태스크를 큐에 대기 하 여 원격 테이블의 인덱스를 조정 하는 방법을 참조 하세요.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 098649587cbb6f01caafdedb631c901af160c85f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87236071"
---
# <a name="syssp_rda_reconcile_indexes-transact-sql"></a>sys. sp_rda_reconcile_indexes (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  원격 테이블의 인덱스를 조정 하는 스키마 태스크를 큐에 대기 시킵니다. 이 작업이 성공적으로 완료 되 면 원격 테이블에는 로컬 스트레치 사용 테이블에 존재 하는 것과 동일한 인덱스가 있습니다.  
  
 **Sp_rda_reconcile_indexes**를 호출할 때 인덱스를 조정 하기 위해 대기 중인 다른 태스크가 있는 경우이 저장 프로시저는 중복 태스크를 큐에 대기 하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>인수  
 [ @objname =] *' objname '*  
 인덱스를 조정 하려는 스트레치 사용 테이블의 정규화 된 이름 또는 정규화 되지 않은 이름입니다. 따옴표는 정규화 된 개체를 지정 하는 경우에만 필요 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0 (성공) 또는 >0 (실패)  
  
## <a name="see-also"></a>참고 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
