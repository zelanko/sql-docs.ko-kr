---
title: sp_db_increased_partitions | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73f3eca2a2e7943d8911144a3657e4f826d9739c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47599135"
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스에 대해 최대 15,000개의 파티션을 지원하도록 설정 또는 해제합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>인수  
 [ @dbname=] '*database_name*'  
 데이터베이스의 이름입니다. *dbname* 됩니다 **sysname** 이며 기본값은 NULL입니다. 하는 경우 *dbname* 지정 하지 않으면 현재 데이터베이스가 사용 됩니다.  
  
 [ @increased_partitions=] '*increased_partitions*'  
 지정된 데이터베이스에서 15,000개의 파티션을 지원하도록 설정 또는 해제합니다. *increased_partitions* 됩니다 **varchar(6)** 이며 기본값은 NULL입니다. 사용 가능한 값은 지원하도록 설정할 경우 'ON' 또는 'TRUE'이고, 지원을 해제할 경우 'OFF' 또는 'FALSE'입니다. 하는 경우 *increased_partitions* 지정 하지 않으면 프로시저는 지정 된 데이터베이스에 대 한 지원 또는 지원을 나타내기 위해 0을 사용 하지 않으면을 나타내려면 1을 반환 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 지정된 데이터베이스에 대한 ALTER DATABASE 권한이 필요합니다.  
  
  
