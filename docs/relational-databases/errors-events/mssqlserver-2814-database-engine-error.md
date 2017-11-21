---
title: "MSSQLSERVER_2814 | Microsoft 문서"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2814 (Database Engine error)
ms.assetid: 22800748-9be9-4511-9428-6b8b40e5bef9
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 109b5a18604b2111f3344ba216a6d3d98131d116
ms.openlocfilehash: 3bca883d9f5b13b81e021014193df43fc3f5f6e3
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="mssqlserver2814"></a>MSSQLSERVER_2814
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2814|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PR_POSSIBLE_INFINITE_RECOMPILE|  
|메시지 텍스트|SQLHANDLE %hs, PlanHandle %hs, 시작 오프셋 %d, 끝 오프셋 %d에 대해 발생 가능한 무한 재컴파일이 검색되었습니다. 마지막 재컴파일 이유는 %d이었습니다.|  
  
## <a name="explanation"></a>설명  
하나 이상의 문으로 인해 쿼리 일괄 처리가 50회 이상 재컴파일되었습니다. 재컴파일이 더 이상 수행되지 않도록 하려면 지정된 문을 수정해야 합니다.  
  
다음 표에서는 재컴파일의 이유를 나열합니다.  
  
|이유 코드|Description|  
|---------------|---------------|  
|1|스키마가 변경됨|  
|2|통계가 변경됨|  
|3|컴파일이 지연됨|  
|4|설정된 옵션이 변경됨|  
|5|임시 테이블이 변경됨|  
|6|원격 행 집합이 변경됨|  
|7|찾아보기 권한이 변경됨|  
|8|쿼리 알림 환경이 변경됨|  
|9|파티션 뷰가 변경됨|  
|10|커서 옵션이 변경됨|  
|11|옵션(recompile)이 요청됨|  
  
## <a name="user-action"></a>사용자 동작  
  
1.  다음 쿼리를 실행하여 재컴파일을 발생시키는 문을 봅니다. *sql_handle*, *starting_offset*, *ending_offset* 및 *plan_handle* 자리 표시자를 오류 메시지에 지정된 값으로 바꿉니다. 임시 및 준비된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우 **database_name** 및 **object_name** 열은 NULL입니다.  
  
    ```sql   
    SELECT DB_NAME(st.dbid) AS database_name,  
        OBJECT_NAME(st.objectid) AS object_name,  
        st.text  
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_sql_text (*sql_handle*) AS st  
    WHERE qs.statement_start_offset = *starting_offset*  
    AND qs.statement_end_offset = *ending_offset*  
    AND qs.plan_handle = *plan_handle*;
    ```
  
2.  이유 코드 설명에 따라 문, 일괄 처리 또는 프로시저를 수정하여 재컴파일을 방지합니다. 예를 들어 저장 프로시저에는 하나 이상의 SET 문이 포함되어 있을 수 있는데, 이러한 문을 프로시저에서 제거해야 합니다. 재컴파일의 원인 및 해결 방법에 대한 추가 예는 [Batch Compilation, Recompilation, and Plan Caching Issues in SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=69175)(SQL Server 2005에서의 일괄 컴파일, 다시 컴파일 및 계획 캐싱 문제)를 참조하세요.  
  
3.  문제가 지속되면 Microsoft 고객 지원 서비스에 문의하십시오.  
  
## <a name="see-also"></a>관련 항목:  
[SQL:StmtRecompile 이벤트 클래스](../event-classes/sql-stmtrecompile-event-class.md)  
  

