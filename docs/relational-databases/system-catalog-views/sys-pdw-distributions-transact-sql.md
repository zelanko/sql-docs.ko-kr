---
description: sys.pdw_distributions (Transact-sql)
title: sys.pdw_distributions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 054dc5391ce03fc079bae505ec3f8fbe2eca2ea2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461594"
---
# <a name="syspdw_distributions-transact-sql"></a>sys.pdw_distributions (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  어플라이언스의 배포에 대 한 정보를 보관 합니다. 여기에는 어플라이언스 배포 당 한 개의 행이 나열 됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|분포와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기의 키입니다.|1은 어플라이언스의 계산 노드 수에 계산 노드당 배포 수를 곱한 값입니다.|  
|pdw_node_id|**int**|이 배포가 설정 된 노드의 ID입니다.|[Sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)에서 pdw_node_id를 참조 하세요.|  
|name|**nvarchar(32)**|분산 테이블에서 접미사로 사용 되는 배포와 관련 된 문자열 식별자입니다.|' A-z ', ' a-z ', ' 0-9 ', ' _ ', '-'로 구성 된 문자열입니다.|  
|position|**int**|노드 내에서 해당 노드의 다른 배포에 대 한 분포의 위치입니다.|노드당 배포 수에 대 한 1입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
