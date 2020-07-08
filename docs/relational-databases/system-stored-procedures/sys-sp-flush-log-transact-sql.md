---
title: sys. sp_flush_log (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cbcb731a4396829b38596619e4b52babcb6f9425
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052728"
---
# <a name="syssp_flush_log-transact-sql"></a>sys.sp_flush_log(Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  현재 데이터베이스의 트랜잭션 로그를 디스크에 플러시하여 이전에 커밋한 지연된 내구성이 있는 트랜잭션이 모두 강화됩니다.  
  
 성능상의 이점 때문에 지연된 트랜잭션 내구성을 사용하도록 선택하지만 서버 충돌이나 장애 조치(Failover) 시 손실되는 데이터 양에 대한 보장 한도도 필요한 경우 정기적으로 `sys.sp_flush_log`를 실행하십시오. 예를 들어 x 초 이상의 데이터가 손실 되지 않도록 하려면 `sp_flush_log` x 초 마다 실행 합니다.  
  
 `sys.sp_flush_log`를 실행하면 이전에 커밋한 지연된 내구성이 있는 트랜잭션이 모두 영구적이 됩니다. 자세한 내용은 개념 항목 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md) 를 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>매개 변수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 반환 코드 1은 성공을 의미합니다.  다른 값은 실패를 의미합니다.  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="sample-code"></a>예제 코드  
  
```sql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  
