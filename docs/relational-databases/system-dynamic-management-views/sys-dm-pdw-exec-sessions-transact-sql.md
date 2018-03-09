---
title: sys.dm_pdw_exec_sessions (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 57fa5867f9fa62dd4a81426673339afcd615f140
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  어플라이언스의 현재 또는 최근에 열린 모든 세션에 대 한 정보를 보유합니다. 세션 마다 하나의 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|현재 쿼리 또는 마지막 쿼리 (세션이 종료 되 고 종료 시 쿼리를 실행 하는) 경우 실행의 id입니다. 이 보기에 대 한 키입니다.|시스템의 모든 세션에서 고유 합니다.|  
|상태|**nvarchar(10)**|현재 세션에 대 한 활성 또는 유휴 세션이 현재는 여부를 식별 합니다. 이전 세션에 대 한 세션 상태를 표시할 수 있습니다 닫혀 있지 않거나 (세션 강제로 끊겼습니다) 하는 경우 종료 합니다.|'ACTIVE', '종료', '유휴 상태', ' 종료 '|  
|request_id|**nvarchar(32)**|현재 쿼리 또는 마지막 쿼리 실행의 id입니다.|시스템의 모든 요청에 대해 고유 합니다. 실행 된 경우 null입니다.|  
|security_id|**varbinary(85)**|보안 세션을 실행 중인 사용자의 ID입니다.||  
|login_name|**nvarchar(128)**|세션을 실행 중인 사용자의 로그인 이름입니다.|사용자 명명 규칙에 맞는 모든 문자열.|  
|login_time|**datetime**|날짜 및 시간을 사용자 로그인 하 고이 세션을 만든입니다.|유효한 **datetime** 현재 시간 이전입니다.|  
|query_count|**int**|만든 후 실행 된 쿼리/requeststhis 세션의 수를 캡처.|보다 크거나 0입니다.|  
|is_transactional|**bit**|세션은 현재 트랜잭션 내에서 아닌지 여부를 캡처합니다.|자동 커밋에 대해 0, 1에 대 한 트랜잭션.|  
|client_id|**nvarchar(255)**|세션에 대 한 클라이언트 정보를 캡처합니다.|유효한 모든 문자열입니다.|  
|app_name|**nvarchar(255)**|필요에 따라 연결 프로세스의 일부로 설정 하는 응용 프로그램 이름 정보를 캡처합니다.|유효한 모든 문자열입니다.|  
|sql_spid|**int**|SPID의 id. 사용 하 여 `session_id` 이 세션입니다. 사용 하 여 `sql_spid` 를 조인 하는 열 **sys.dm_pdw_nodes_exec_sessions**합니다.<br /><br /> **\*\*경고 \* \***  닫힌된 Spid이이 열을 포함 합니다.||  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에 최대 시스템 뷰의 값 섹션을 참조는 [최소값 및 최 댓 값 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) 항목입니다.  
  
## <a name="permissions"></a>Permissions  
 필요는 `VIEW SERVER STATE` 권한.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
