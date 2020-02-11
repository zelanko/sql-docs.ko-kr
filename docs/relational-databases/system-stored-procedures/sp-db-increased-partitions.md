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
ms.openlocfilehash: 83a40c9070db1c997f30db71a6cff226cd0430d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108261"
---
# <a name="sp_db_increased_partitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스에 대해 최대 15,000개의 파티션을 지원하도록 설정 또는 해제합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>인수  
 [ @dbname= ] '*database_name*'  
 데이터베이스의 이름입니다. *dbname* 은 **sysname** 이며 기본값은 NULL입니다. *Dbname* 을 지정 하지 않으면 현재 데이터베이스가 사용 됩니다.  
  
 [ @increased_partitions= ] '*increased_partitions*'  
 지정된 데이터베이스에서 15,000개의 파티션을 지원하도록 설정 또는 해제합니다. *increased_partitions* 는 **varchar (6)** 이며 기본값은 NULL입니다. 사용 가능한 값은 지원하도록 설정할 경우 'ON' 또는 'TRUE'이고, 지원을 해제할 경우 'OFF' 또는 'FALSE'입니다. *Increased_partitions* 지정 하지 않으면 지정 된 데이터베이스에 대 한 지원이 사용 하도록 설정 되었음을 나타내는 1이 프로시저에서 1을 반환 하 고, 지원 기능을 사용 하지 않음을 나타내는 0을 반환 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 지정된 데이터베이스에 대한 ALTER DATABASE 권한이 필요합니다.  
  
  
