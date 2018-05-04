---
title: sys.dm_pdw_dms_cores (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b3f09b15-0863-4418-9347-a4f5fd2ab7c7
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 91b89298aaa6030456c054adbd0e584a07b89288
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwdmscores-transact-sql"></a>sys.dm_pdw_dms_cores (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  어플라이언스의 계산 노드에서 실행 되는 모든 DMS 서비스에 대 한 정보를 보유 합니다. 노드당 하나의 행이 현재는 서비스 인스턴스의 당 한 개의 행을 나열 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|**int**|이 DMS 코어와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기에 대 한 키입니다.|이 DMS 코어에서 실행 되는 노드의 pdw_node_id로 설정 합니다.|  
|pdw_node_id|**int**|이 DMS 서비스 실행 되는 노드의 ID입니다.|참조에 대 한 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|상태|**nvarchar(32)**|DMS 서비스의 현재 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에 최대 시스템 뷰의 값 섹션을 참조는 [최소값 및 최 댓 값 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) 항목입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
