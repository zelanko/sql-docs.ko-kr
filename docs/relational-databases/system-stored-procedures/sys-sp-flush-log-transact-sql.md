---
title: sys.sp_flush_log (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 2dad71f88311c8a44a03ab48ae4ad2daab1c3709
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031535"
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 트랜잭션 로그를 디스크에 플러시하여 이전에 커밋한 지연된 내구성이 있는 트랜잭션이 모두 강화됩니다.  
  
 성능상의 이점 때문에 지연된 트랜잭션 내구성을 사용하도록 선택하지만 서버 충돌이나 장애 조치(Failover) 시 손실되는 데이터 양에 대한 보장 한도도 필요한 경우 정기적으로 `sys.sp_flush_log`를 실행하십시오. 예를 들어, 손실되는 데이터를 x초 이하로 제한하려는 경우 x초마다 `sp_flush_log`를 실행합니다.  
  
 `sys.sp_flush_log`를 실행하면 이전에 커밋한 지연된 내구성이 있는 트랜잭션이 모두 영구적이 됩니다. 개념 항목을 참조 하세요 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md) 자세한 내용은 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
  
