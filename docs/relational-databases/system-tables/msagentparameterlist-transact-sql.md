---
title: MSagentparameterlist (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f03817f9e7b13e21eb7513de4a4d96216b700460
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890066"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Msagentparameterlist** 테이블은 복제 에이전트 매개 변수 정보를 포함 하며 지정 된 에이전트 유형에 설정할 수 있는 매개 변수를 지정 하는 데 사용 됩니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|에이전트의 유형입니다.<br /><br /> **1** = 스냅숏 에이전트.<br /><br /> **2** = 로그 판독기 에이전트.<br /><br /> **3** = 배포 에이전트.<br /><br /> **4** = 병합 에이전트.<br /><br /> **9** = 큐 판독기 에이전트.|  
|**parameter_name**|**sysname**|유효한 에이전트 매개 변수의 이름입니다.|  
|**default_value**|**nvarchar(4000)**|에이전트 매개 변수의 기본값입니다. NULL은 기본값이 없음을 나타냅니다.|  
|**min_value**|**int**|에이전트 매개 변수의 하한을 설정합니다. NULL은 하한이 없음을 나타냅니다.|  
|**max_value**|**int**|에이전트 매개 변수의 상한을 설정합니다. NULL은 상한이 없음을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
