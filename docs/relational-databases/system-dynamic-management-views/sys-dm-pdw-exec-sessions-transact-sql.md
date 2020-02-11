---
title: sys. dm_pdw_exec_sessions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4d559f7fb03b632fc5cfca573b2fedc72506fead
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899404"
---
# <a name="sysdm_pdw_exec_sessions-transact-sql"></a>sys. dm_pdw_exec_sessions (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  어플라이언스에서 현재 또는 최근에 열려 있는 모든 세션에 대 한 정보를 보관 합니다. 세션 마다 하나의 행을 나열 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar (32)**|현재 쿼리 또는 마지막 쿼리 실행의 id입니다 (세션이 종료 되 고 종료 시 쿼리가 실행 되는 경우). 이 보기의 키입니다.|시스템의 모든 세션에서 고유 합니다.|  
|상태|**nvarchar (10)**|현재 세션의 경우 세션이 현재 활성 상태 인지 아니면 유휴 상태 인지를 식별 합니다. 이전 세션의 경우 세션 상태는 종료 됨 또는 중단 됨으로 표시 될 수 있습니다 (세션이 강제로 닫혀 있는 경우).|' ACTIVE ', ' CLOSED ', ' IDLE ', ' 종료 됨 '|  
|request_id|**nvarchar (32)**|현재 쿼리 또는 마지막 쿼리 실행의 id입니다.|시스템의 모든 요청에 대해 고유 합니다. 실행 된 항목이 없으면 Null입니다.|  
|security_id|**varbinary (85)**|세션을 실행 하는 보안 주체의 보안 ID입니다.||  
|login_name|**nvarchar(128)**|세션을 실행 하는 보안 주체의 로그인 이름입니다.|사용자 명명 규칙을 준수 하는 문자열입니다.|  
|login_time|**datetime**|사용자가 로그인 하 고이 세션을 만든 날짜 및 시간입니다.|현재 시간 이전의 유효한 **날짜/** 시간입니다.|  
|query_count|**int**|생성 이후 실행 된 쿼리 수를 캡처합니다.|0 보다 크거나 같습니다.|  
|is_transactional|**bit**|세션이 현재 트랜잭션 내에 있는지 여부를 캡처합니다.|자동 커밋의 경우 0, 트랜잭션의 경우 1입니다.|  
|client_id|**nvarchar(255)**|세션에 대 한 클라이언트 정보를 캡처합니다.|모든 유효한 문자열입니다.|  
|app_name|**nvarchar(255)**|선택적으로 연결 프로세스의 일부로 설정 된 응용 프로그램 이름 정보를 캡처합니다.|모든 유효한 문자열입니다.|  
|sql_spid|**int**|SPID의 id 번호입니다. 이 세션 `session_id` 을 사용 합니다. `sql_spid` 열을 사용 하 여 **dm_pdw_nodes_exec_sessions**에 조인 합니다.<br /><br /> ** \* 경고 \* \* ** 이 열에는 닫힌 Spid가 포함 됩니다.||  
  
 이 보기에 의해 유지 되는 최대 행에 대 한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목에서 메타 데이터 섹션을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 `VIEW SERVER STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
