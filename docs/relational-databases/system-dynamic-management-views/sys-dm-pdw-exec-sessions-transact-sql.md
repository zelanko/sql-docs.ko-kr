---
title: sys.dm_pdw_exec_sessions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f8d910bc9b6d85475a937940787aec7a312ef3bf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781171"
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  어플라이언스에서 현재 또는 최근에 열린 모든 세션에 대 한 정보를 보유합니다. 세션당 행 하나를 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|Id는 현재 쿼리 또는 마지막 쿼리 실행 (의 세션을 종료 하 고 쿼리 종료 시 실행 된) 경우입니다. 이 보기에 대 한 키입니다.|시스템의 모든 세션에서 고유 합니다.|  
|상태|**nvarchar(10)**|현재 세션에 대 한 활성 또는 유휴 세션이 현재 인지 여부를 식별 합니다. 이전 세션에 대 한 세션 상태 표시 될 수 있습니다 닫히거나 (세션이 강제로 닫혔습니다) 하는 경우 종료 합니다.|'ACTIVE', 'CLOSED', '유휴 상태', ' 종료 '|  
|request_id|**nvarchar(32)**|현재 쿼리 또는 마지막 쿼리 실행의 id입니다.|시스템의 모든 요청에서 고유 합니다. 실행 된 경우 null입니다.|  
|security_id|**varbinary(85)**|세션이 실행 되는 보안 주체의 보안 ID입니다.||  
|login_name|**nvarchar(128)**|세션을 실행 하는 사용자의 로그인 이름입니다.|사용자 이름 지정 규칙을 따르는 문자열입니다.|  
|login_time|**datetime**|날짜 및는 사용자가 로그인 하 고이 세션을 만든 시간입니다.|유효한 **날짜/시간** 현재 시간 이전입니다.|  
|query_count|**int**|캡처를 만든 후 실행 된 쿼리/requeststhis 세션의 수입니다.|보다 크거나 0입니다.|  
|is_transactional|**bit**|세션은 현재 트랜잭션 내에서 인지 여부를 캡처합니다.|자동 커밋에 대 한 0, 1에 대 한 트랜잭션.|  
|client_id|**nvarchar(255)**|세션에 대 한 클라이언트 정보를 캡처합니다.|모든 유효한 문자열입니다.|  
|app_name|**nvarchar(255)**|필요에 따라 연결 프로세스의 일부로 설정 하는 응용 프로그램 이름 정보를 캡처합니다.|모든 유효한 문자열입니다.|  
|sql_spid|**int**|SPID의 id. 사용 된 `session_id` 이 세션입니다. 사용 된 `sql_spid` 열을 조인할 **sys.dm_pdw_nodes_exec_sessions**.<br /><br /> **\*\* 경고 \* \***  이 열에 닫힌된 Spid를 포함 합니다.||  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에서 최대 시스템 뷰의 값 섹션을 참조 합니다 [최소값 및 최대값 (SQL Server PDW)](http://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9) 항목입니다.  
  
## <a name="permissions"></a>사용 권한  
 `VIEW SERVER STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
