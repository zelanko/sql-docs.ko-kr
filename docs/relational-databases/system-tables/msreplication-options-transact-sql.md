---
description: MSreplication_options(Transact-SQL)
title: MSreplication_options (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 096eb8379363e3a193ecea12593638e033c3b1ec
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538243"
---
# <a name="msreplication_options-transact-sql"></a>MSreplication_options(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplication_options** 테이블은 복제에 의해 내부적으로 사용 되는 메타 데이터를 저장 합니다. 이 테이블은 **master** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|내부적으로만 사용됩니다.|  
|**value**|**bit**|내부적으로만 사용됩니다.|  
|**major_version**|**int**|내부적으로만 사용됩니다.|  
|**minor_version**|**int**|내부적으로만 사용됩니다.|  
|**revision**|**int**|내부적으로만 사용됩니다.|  
|**install_failures**|**int**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
