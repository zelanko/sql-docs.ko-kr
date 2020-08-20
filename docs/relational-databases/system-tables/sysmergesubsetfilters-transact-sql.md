---
description: sysmergesubsetfilters(Transact-SQL)
title: sysmergesubsetfilters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubsetfilters
- sysmergesubsetfilters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubsetfilters system table
ms.assetid: f91d1c6c-3132-47f6-926c-88f56848cafe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7257cd9ab4de29343015fa1050c336d3e8a69e65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485443"
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  분할된 아티클의 조인 필터 정보를 포함합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**filtername**|**sysname**|아티클을 만드는 데 사용되는 필터의 이름입니다.|  
|**join_filterid**|**int**|조인 필터를 나타내는 개체의 ID입니다.|  
|**pubid**|**uniqueidentifier**|게시의 ID입니다.|  
|**artid**|**uniqueidentifier**|아티클의 ID입니다.|  
|**art_nickname**|**int**|아티클의 애칭입니다.|  
|**join_articlename**|**sysname**|행이 속하는지 여부를 결정하도록 조인할 테이블의 이름입니다.|  
|**join_nickname**|**int**|행이 속하는지 여부를 결정하기 위해 조인할 테이블의 애칭입니다.|  
|**join_unique_key**|**int**|**Join_tablename**의 고유 키에 대 한 조인을 나타냅니다.<br /><br /> 0 = 고유 키가 아닙니다.<br /><br /> 1 = 고유 키입니다.|  
|**expand_proc**|**sysname**|병합 에이전트가 구독자에서 보내지거나 제거될 필요가 있는 행을 식별하는 데 사용되는 저장 프로시저의 이름입니다.|  
|**join_filterclause**|**nvarchar(1000)**|조인에 사용되는 필터 절입니다.|  
|**filter_type**|**tinyint**|필터 유형을 지정하며 다음 중 하나일 수 있습니다.<br /><br /> 1 = 조인 필터.<br /><br /> 2 = 논리적 레코드 링크.<br /><br /> 3 = 조인 필더 및 논리적 레코드 링크 모두.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
