---
title: _pdw_nodes_exec_sql_text (Transact-sql) | Microsoft Docs
description: 지정 된 sql_handle으로 식별 되는 SQL 일괄 처리의 텍스트를 반환 하는 동적 관리 뷰입니다.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: fd886217b2fb2caf0fe3f32e88b7bf0215ece1a9
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145678"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>_nodes_dm_exec_sql_text (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

지정 된 *sql_handle*으로 식별 되는 SQL 일괄 처리의 텍스트를 반환 합니다. 이 테이블 반환 함수는 시스템 함수 **fn_get_sql**을 대체 합니다.  
   
## <a name="table-returned"></a>반환 된 테이블  
|열 이름|이름|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|노드와 연결 된 고유 숫자 ID입니다.|
|**dbid**|**smallint**|데이터베이스의 ID입니다.<br /><br /> 계획 되지 않은 SQL 문 및 준비 된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.|  
|**objectid**|**int**|개체의 ID입니다.<br /><br /> 임시 및 준비된 SQL 문의 경우 NULL입니다.|  
|**number**|**smallint**|번호가 있는 저장 프로시저의 경우 저장 프로시저의 번호가 이 열에 반환됩니다. 자세한 내용은 [numbered_procedures &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)을 참조 하세요.<br /><br /> 임시 및 준비된 SQL 문의 경우 NULL입니다.|  
|**encrypted**|**bit**|1: SQL 텍스트가 암호화 됩니다.<br /><br /> 0: SQL 텍스트가 암호화 되지 않습니다.|  
|**text**|**nvarchar(max)**|SQL 쿼리의 텍스트입니다.<br /><br /> 암호화된 개체의 경우 NULL입니다.|  

## <a name="remarks"></a>Remarks  
[_Exec_sql_text](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql?view=sql-server-ver15) 에 동일한 설명이 적용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 서버에 대 한 **sysadmin** 서버 역할 또는 `VIEW SERVER STATE` 권한이 필요 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>다음 단계
 더 많은 개발 팁은 [SQL Data Warehouse 개발 개요](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)를 참조 하세요.