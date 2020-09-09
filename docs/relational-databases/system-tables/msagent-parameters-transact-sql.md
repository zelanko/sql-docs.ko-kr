---
description: MSagent_parameters(Transact-SQL)
title: MSagent_parameters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_parameters_TSQL
- MSagent_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_parameters system table
ms.assetid: be30abc9-c00d-446f-b1b4-1269772f37e6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f462e59611b33d35762ad0941e871c196990f2c5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544546"
---
# <a name="msagent_parameters-transact-sql"></a>MSagent_parameters(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSagent_parameters** 테이블에는 에이전트 프로필과 연결 된 매개 변수가 포함 되어 있습니다. 매개 변수 이름은 에이전트에서 지원되는 것과 동일합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|**MSagent_profiles** 테이블의 프로필 ID입니다.|  
|**parameter_name**|**sysname**|매개 변수의 이름입니다.|  
|**value**|**nvarchar(255)**|매개 변수의 값입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
