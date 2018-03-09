---
title: SET QUERY_GOVERNOR_COST_LIMIT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT
- SET_QUERY_GOVERNOR_COST_LIMIT_TSQL
- QUERY_GOVERNOR_COST_LIMIT
- QUERY_GOVERNOR_COST_LIMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT statement
- connections [SQL Server], overriding
- QUERY_GOVERNOR_COST_LIMIT option
- overriding connection values
ms.assetid: 3424bb44-6915-462d-a8d7-fe834af81387
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a96642c6a0dd50ccb8717e84a6defec516196d87
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="set-querygovernorcostlimit-transact-sql"></a>SET QUERY_GOVERNOR_COST_LIMIT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 구성 된 재정의 **쿼리 관리자 비용 제한** 현재 연결에 대 한 값입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET QUERY_GOVERNOR_COST_LIMIT value  
```  
  
## <a name="arguments"></a>인수  
 *value*  
 쿼리가 실행될 수 있는 가장 긴 시간을 지정하는 숫자 또는 정수 값입니다. 값을 가장 가까운 정수로 내림합니다. 음수 값은 0으로 올림됩니다. 쿼리 관리자는 예상 비용이 해당 값을 초과하는 쿼리의 실행을 허용하지 않습니다. 이 옵션에 0(기본값)을 지정하면 쿼리 관리자가 꺼지고 모든 쿼리가 무기한 실행될 수 있습니다.  
  
 "쿼리 비용"이란 특정 하드웨어 구성에서 쿼리를 완료하는 데 필요한 예상 소요 시간(초)입니다.  
  
## <a name="remarks"></a>주의  
 SET QUERY_GOVERNOR_COST_LIMIT 옵션은 현재 연결에만 적용되며 현재 연결 기간 동안 지속됩니다. 사용 하 여는 [query governor cost limit 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)옵션의 **sp_configure** 변경할 서버 차원의 쿼리 관리자 비용 제한 값입니다. 이 옵션을 구성 하는 방법에 대 한 자세한 내용은 참조 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 및 [서버 구성 옵션 &#40; SQL Server &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 SET QUERY_GOVERNOR_COST_LIMIT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
