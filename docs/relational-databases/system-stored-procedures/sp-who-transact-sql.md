---
title: sp_who (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_who_TSQL
- sp_who
dev_langs:
- TSQL
helpviewer_keywords:
- sp_who
ms.assetid: 132dfb08-fa79-422e-97d4-b2c4579c6ac5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d748f06a592283c49d85624c97f4db7afdc188e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628961"
---
# <a name="spwho-transact-sql"></a>sp_who(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 사용자, 세션 및 인스턴스의 프로세스 정보를 제공 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]합니다. 유휴 상태가 아닌 프로세스, 특정 사용자에게 속한 프로세스 또는 특정 세션에 속하는 프로세스만 반환하도록 이 정보를 필터링할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_who [ [ @loginame = ] 'login' | session ID | 'ACTIVE' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@loginame =** ] **'***로그인***'** | *세션 ID* | **'ACTIVE'**  
 결과 세트를 필터링하는 데 사용됩니다.  
  
 *로그인* 됩니다 **sysname** 특정 로그인에 속하는 프로세스를 식별 하는 합니다.  
  
 *세션 ID* 속하는 세션 id 입니다는는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스. *세션 ID* 됩니다 **smallint**합니다.  
  
 **활성** 사용자 로부터 다음 명령에 대 한 대기 중인 세션을 제외 합니다.  
  
 값을 지정하지 않으면 인스턴스에 속하는 모든 세션이 보고됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 **sp_who** 결과 다음 정보를 사용 하 여 집합을 반환 합니다.  
  
|Column|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**spid**|**smallint**|세션 ID입니다.|  
|**ecid**|**smallint**|특정 세션 ID와 연결된 지정된 스레드의 실행 컨텍스트 ID입니다.<br /><br /> ECID = {0, 1, 2, 3,... *n*} 이며 여기서 0은 항상 주 또는 부모 스레드를 하 고 {1, 2, 3,... *n*} 의미 합니다.|  
|**상태**|**nchar(30)**|프로세스 상태입니다. 가능한 값은 아래와 같습니다.<br /><br /> **유휴**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 세션을 다시 설정하고 있습니다.<br /><br /> **실행**합니다. 세션에서 일괄 처리를 하나 이상 실행하고 있습니다. MARS(Multiple Active Result Sets)를 설정하면 세션에서 여러 개의 일괄 처리를 실행할 수 있습니다. 자세한 내용은 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조하세요.<br /><br /> **백그라운드**합니다. 세션에서 교착 상태 감지와 같은 백그라운드 태스크를 실행하고 있습니다.<br /><br /> **롤백**합니다. 세션에서 트랜잭션 롤백을 진행하고 있습니다.<br /><br /> **보류 중인**합니다. 세션이 작업자 스레드를 사용할 수 있을 때까지 기다리고 있습니다.<br /><br /> **실행 가능한**합니다. 세션의 태스크는 시간 퀀텀을 얻기 위해 기다리는 동안 스케줄러의 실행 가능한 큐에 있습니다.<br /><br /> **spinloop**합니다. 세션의 태스크가 spinlock을 사용할 수 있을 때까지 기다리고 있습니다.<br /><br /> **일시 중단**합니다. 세션이 I/O와 같은 이벤트가 완료되기를 기다리고 있습니다.|  
|**loginame**|**nchar(128)**|특정 프로세스와 연결된 로그인 이름입니다.|  
|**호스트 이름**|**nchar(128)**|각 프로세스의 호스트 또는 컴퓨터 이름입니다.|  
|**blk**|**char(5)**|프로세스를 차단하기 위한 세션 ID입니다(존재하는 경우). 없는 경우 이 열은 0이 됩니다.<br /><br /> 분리된 분산 트랜잭션이 지정된 세션 ID와 연결된 트랜잭션을 차단하는 경우 이 열은 분리된 트랜잭션을 차단하기 위한 값으로 '-2'를 반환합니다.|  
|**dbname**|**nchar(128)**|프로세스가 사용하는 데이터베이스입니다.|  
|**cmd**|**nchar(16)**|프로세스에 대해 실행 중인 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 명령([!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 내부 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로세스 등)입니다.|  
|**request_id**|**int**|특정 세션에서 실행 중인 요청에 대한 ID입니다.|  
  
 병렬 처리의 경우 특정 세션 ID에 대해 하위 스레드가 생성됩니다. 주 스레드는 `spid = <xxx>` 및 `ecid =0`으로 표시됩니다. 다른 하위 스레드의 동일 `spid = <xxx>`, 하지만 **ecid** > 0입니다.  
  
## <a name="remarks"></a>Remarks  
 차단 프로세스(배타 잠금이 설정된 경우도 있음)는 다른 프로세스에 필요한 리소스를 보유하고 있는 프로세스입니다.  
  
 모든 분리된 분산 트랜잭션에는 세션 ID 값 '-2'가 할당됩니다. 분리된 분산 트랜잭션은 어떤 세션 ID와도 연결되지 않은 분산 트랜잭션입니다. 자세한 내용은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)을 참조하세요.  
  
 쿼리는 **is_user_process** 사용자 프로세스에서 시스템 프로세스를 분리 하는 sys.dm_exec_sessions의 열입니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 실행되는 모든 세션을 볼 수 있으려면 해당 서버에 대한 VIEW SERVER STATE 권한이 필요합니다. 그렇지 않으면 현재 세션만 사용자에게 표시됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-all-current-processes"></a>1. 현재 프로세스 모두 나열  
 다음 예에서는 매개 변수 없이 `sp_who`를 사용하여 현재 사용자를 모두 보고합니다.  
  
```  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
### <a name="b-listing-a-specific-users-process"></a>2. 특정 사용자의 프로세스 나열  
 다음 예에서는 로그인 이름으로 한 명의 현재 사용자에 대한 정보를 보는 방법을 보여 줍니다.  
  
```  
USE master;  
GO  
EXEC sp_who 'janetl';  
GO  
```  
  
### <a name="c-displaying-all-active-processes"></a>3. 활성 프로세스 모두 표시  
  
```  
USE master;  
GO  
EXEC sp_who 'active';  
GO  
```  
  
### <a name="d-displaying-a-specific-process-identified-by-a-session-id"></a>4. 세션 ID를 지정하여 특정 프로세스 표시  
  
```  
USE master;  
GO  
EXEC sp_who '10' --specifies the process_id;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sys.sysprocesses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
