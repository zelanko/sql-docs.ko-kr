---
title: sys.sp_rda_reconcile_indexes (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3f020a11a0fa41d7cbd939279058e9292c5d488c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdareconcileindexes-transact-sql"></a>sys.sp_rda_reconcile_indexes (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  원격 테이블의 인덱스를 조정 하는 스키마 작업을 큐에 넣습니다. 이 작업이 성공적으로 완료 되 면 원격 테이블의 로컬 스트레치 사용 테이블에 존재 하는 동일한 인덱스 설정 됩니다.  
  
 다른 작업을 호출 하는 경우 인덱스를 조정 하려면 대기 **sp_rda_reconcile_indexes**,이 저장된 프로시저는 중복 작업을 큐 대기 하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>인수  
 [@objname =] *'objname'*  
 인덱스를 조정 하려는 스트레치 사용 테이블의 정규화 되거나 정규화 되지 않은 이름이입니다. 따옴표는 정규화 된 개체를 지정 하는 경우에 필요 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 >0(실패)  
  
## <a name="see-also"></a>관련 항목:  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
