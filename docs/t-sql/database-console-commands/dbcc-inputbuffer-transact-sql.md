---
title: DBCC INPUTBUFFER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
caps.latest.revision: 51
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 54e4c8309c290255cb2885fab04bb394bc453046
ms.openlocfilehash: 3d9b6acfbfef3125d6ee715708492de1cae2b3a2
ms.contentlocale: ko-kr
ms.lasthandoff: 10/16/2017

---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

인스턴스를 클라이언트에서 보낸 마지막 문 표시 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
*session_id*  
각 기본 활성 연결과 연관된 세션 ID입니다.  
  
*request_id*  
현재 세션 내에서 검색할 정확한 요청(일괄 처리)입니다.  

다음 쿼리에서 반환 *request_id*:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
의 모든 멘션을  
지정할 옵션을 활성화합니다.  
  
NO_INFOMSGS  
심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="result-sets"></a>결과 집합  
DBCC INPUTBUFFER는 다음과 같은 열이 있는 행 집합을 반환합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**이벤트 유형**|**nvarchar (30)**|이벤트 유형입니다. 이 수 **RPC 이벤트** 또는 **언어 이벤트**합니다. 출력 됩니다 **No Event** 마지막 이벤트가 발견 된 경우.|  
|**매개 변수**|**smallint**|0 = 텍스트<br /><br /> 1-  *n*  = 매개 변수|  
|**EventInfo**|**nvarchar(4000)**|에 대 한 프로그램 **EventType** RPC의 **EventInfo** 프로시저 이름만 포함 합니다. 에 대 한 프로그램 **EventType** 언어에서의 이벤트의 첫 4000 자만 표시 됩니다.|  
  
예를 들어 DBCC INPUTBUFFER는 버퍼의 마지막 이벤트가 DBCC INPUTBUFFER(11)인 경우에 다음과 같은 결과 집합을 반환합니다.
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> 부터는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] s p 2를 사용 하 여 [sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) 의 인스턴스에 제출 된 문에 대 한 정보를 반환할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

## <a name="permissions"></a>Permissions  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 중 하나가 필요 합니다.
-   사용자의 구성원 이어야 합니다.는 **sysadmin** 고정된 서버 역할입니다.  
-   사용자에게 VIEW SERVER STATE 권한이 있어야 합니다.  
-   *session_id* 명령이 실행 되 고 세션 ID과 같아야 합니다. 세션 ID를 확인하려면 다음 쿼리를 실행합니다.  
  
```sql
SELECT @@spid;  
```
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 프리미엄 계층 데이터베이스에서 VIEW DATABASE STATE 권한이 필요 합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 표준 및 기본 계층 필요는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 관리자 계정.
  
## <a name="examples"></a>예  
다음 예에서는 이전 연결에서 긴 트랜잭션이 실행되는 동안 두 번째 연결에서 `DBCC INPUTBUFFER`를 실행합니다.
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  

