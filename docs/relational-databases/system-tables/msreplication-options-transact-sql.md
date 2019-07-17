---
title: MSreplication_options (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: stevestein
ms.author: sstein
ms.openlocfilehash: c48a57b876cde41d6bb514c522bcaa241eec11fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062999"
---
# <a name="msreplicationoptions-transact-sql"></a>MSreplication_options(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSreplication_options** 테이블은 복제에 의해 내부적으로 사용 되는 메타 데이터를 저장 합니다. 이 테이블에 저장 되는 **마스터** 데이터베이스입니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|내부적으로만 사용됩니다.|  
|**value**|**bit**|내부적으로만 사용됩니다.|  
|**major_version**|**int**|내부적으로만 사용됩니다.|  
|**minor_version**|**int**|내부적으로만 사용됩니다.|  
|**revision**|**int**|내부적으로만 사용됩니다.|  
|**install_failures**|**int**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
