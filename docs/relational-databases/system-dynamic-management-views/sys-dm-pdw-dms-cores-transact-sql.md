---
title: sys.dm_pdw_dms_cores (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b3f09b15-0863-4418-9347-a4f5fd2ab7c7
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 76a154639a71b22bfe3f119233f3abbcd329f7c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899523"
---
# <a name="sysdmpdwdmscores-transact-sql"></a>sys.dm_pdw_dms_cores (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  어플라이언스의 계산 노드에서 실행 중인 모든 DMS 서비스에 대 한 정보를 보유 합니다. 노드당 하나의 행이 현재 서비스 인스턴스마다 하나의 행을 나열 합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|**int**|이 DMS 코어를 사용 하 여 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기에 대 한 키입니다.|이 DMS core에서 실행 되는 노드의 pdw_node_id로 설정 합니다.|  
|pdw_node_id|**int**|DMS 서비스가 실행 되는 노드의 ID입니다.|에 대 한 node_id를 참조 하세요 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|상태|**nvarchar(32)**|DMS 서비스의 현재 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에서 메타 데이터 섹션을 참조 합니다 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목입니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
