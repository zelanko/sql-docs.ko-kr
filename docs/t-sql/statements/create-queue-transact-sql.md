---
title: CREATE QUEUE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUEUE_TSQL
- CREATE QUEUE
- QUEUE
- CREATE_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE QUEUE statement
- internal activation [Service Broker]
- stored procedure activation [Service Broker]
- message retention [Service Broker]
- unavailable queues [Service Broker]
- activation stored procedures [Service Broker]
- queues [Service Broker], creating
ms.assetid: fce80faf-2bdc-475d-8ca1-31438ed41fb0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8247b0fe0e17ae717fddd89ff4a608481e0777ad
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634005"
---
# <a name="create-queue-transact-sql"></a>CREATE QUEUE(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

데이터베이스에 새 큐를 만듭니다. 큐는 메시지를 저장합니다. 서비스에 대한 메시지가 도착하면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 이 메시지를 서비스에 연결된 큐에 넣습니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
CREATE QUEUE <object>
   [ WITH
     [ STATUS = { ON | OFF } [ , ] ]
     [ RETENTION = { ON | OFF } [ , ] ]
     [ ACTIVATION (
         [ STATUS = { ON | OFF } , ]
           PROCEDURE_NAME = <procedure> ,
           MAX_QUEUE_READERS = max_readers ,
           EXECUTE AS { SELF | 'user_name' | OWNER }
            ) [ , ] ]
     [ POISON_MESSAGE_HANDLING (
         [ STATUS = { ON | OFF } ] ) ]
    ]
     [ ON { filegroup | [ DEFAULT ] } ]
[ ; ]

<object> ::=
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }

<procedure> ::=
{ database_name.schema_name.stored_procedure_name | schema_name.stored_procedure_name | stored_procedure_name }

```

## <a name="arguments"></a>인수

*database_name*(개체)은 새 큐를 만들 데이터베이스의 이름입니다. *database_name*은 기존 데이터베이스 이름을 지정해야 합니다. *database_name*을 지정하지 않으면 현재 데이터베이스에 큐가 만들어집니다.

*schema_name*(개체)은 새로운 큐가 속할 스키마 이름입니다. 기본 스키마는 문을 실행하는 사용자의 기본 스키마입니다. *database_name*으로 지정된 데이터베이스에서 sysadmin 고정 서버 역할의 멤버나 db_dbowner 또는 db_ddladmin 고정 데이터베이스 역할의 멤버가 CREATE QUEUE 문을 실행한 경우 *schema_name*은 현재 연결의 로그인에 연결된 스키마 이외의 스키마를 지정할 수 있습니다. 그렇지 않으면 *schema_name*은 문을 실행하는 사용자의 기본 스키마여야 합니다.

*queue_name*은 만들 큐의 이름입니다. 이 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자에 적용되는 지침을 준수해야 합니다.

STATUS(큐)는 큐의 사용 가능 여부(ON 또는 OFF)를 지정합니다. 큐를 사용할 수 없을 경우 큐에서 메시지를 추가하거나 제거할 수 없습니다. ALTER QUEUE 문으로 큐를 사용할 수 있게 설정할 때까지 메시지가 큐에 도착하지 않도록 하기 위해 사용할 수 없는 상태의 큐를 만들 수 있습니다. 이 절을 생략하면 기본값은 ON이며 큐를 사용할 수 있습니다.

RETENTION은 큐에 대한 보존 설정을 지정합니다. RETENTION = ON인 경우 이 큐의 대화에서 주고 받은 모든 메시지가 대화가 끝날 때까지 큐에 남아 있습니다. 그러므로 오류가 발생할 때 보정 트랜잭션을 수행하기 위해 또는 감사할 목적으로 메시지를 유지할 수 있습니다. 이 절을 지정하지 않은 경우 보존 설정의 기본값은 OFF입니다.

> [!NOTE]
> RETENTION = ON으로 설정하면 성능이 저하될 수 있습니다. 이 설정은 애플리케이션에 필요한 경우에만 사용해야 합니다.

ACTIVATION은 이 큐에 있는 메시지를 처리하기 위해 시작해야 하는 저장 프로시저에 대한 정보를 지정합니다.

STATUS(활성화)는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 저장 프로시저를 시작할지 여부를 지정합니다. STATUS = ON이면 현재 실행 중인 프로시저 수가 MAX_QUEUE_READERS보다 작고, 큐에 도착하는 메시지가 저장 프로시저의 메시지 수신 속도보다 빠른 경우 큐에서 PROCEDURE_NAME에 지정된 저장 프로시저를 시작합니다. STATUS = OFF이면 큐에서 저장 프로시저를 시작하지 않습니다. 이 절을 지정하지 않은 경우 기본값은 ON입니다.

PROCEDURE_NAME = \<procedure>은 이 큐에 있는 메시지를 처리하기 위해 시작할 저장 프로시저의 이름을 지정합니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자여야 합니다.

*database_name*(프로시저)은 저장 프로시저가 포함된 데이터베이스의 이름입니다.

*schema_name*(프로시저)은 저장 프로시저가 포함된 스키마의 이름입니다.

*procedure_name*은 저장 프로시저의 이름입니다.

MAX_QUEUE_READERS =*max_readers*는 큐에서 동시에 시작하는 활성화 저장 프로시저의 최대 인스턴스 수를 지정합니다. *max_readers*의 값은 **0**에서 **32767** 사이의 숫자여야 합니다.

EXECUTE AS는 활성화 저장 프로시저를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 계정을 지정합니다. 큐에서 저장 프로시저를 시작할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 사용자의 권한을 확인할 수 있어야 합니다. 도메인 사용자의 경우 프로시저를 시작할 때 서버가 도메인에 연결되어 있어야 합니다. 그렇지 않으면 활성화가 실패합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자의 경우에는 서버에서 항상 권한을 확인할 수 있습니다.

SELF는 저장 프로시저가 현재 사용자로 실행되도록 지정합니다(이 CREATE QUEUE 문을 실행하는 데이터베이스 보안 주체).

'*user_name*'은 저장 프로시저가 실행되는 사용자의 이름입니다. *user_name* 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자로 지정된 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자여야 합니다. 현재 사용자에게 지정한 *user_name*에 대한 IMPERSONATE 권한이 있어야 합니다.

OWNER는 저장 프로시저가 큐의 소유자로 실행되도록 지정합니다.

POISON_MESSAGE_HANDLING은 큐에 대해 포이즌 메시지 처리를 사용하는지 여부를 지정합니다. 기본값은 ON입니다.

포이즌 메시지 처리가 OFF로 설정된 큐는 트랜잭션 롤백이 연속으로 5회 발생하더라도 비활성화되지 않습니다. 이렇게 하면 애플리케이션에서 사용자 지정 포이즌 메시지 처리 시스템을 정의할 수 있습니다.

ON *filegroup |* [**DEFAULT**]는 이 큐를 만들 파일 그룹[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 지정합니다. *filegroup* 매개 변수를 사용하여 파일 그룹을 지정하거나 DEFAULT 식별자를 사용하여 Service Broker 데이터베이스의 기본 파일 그룹을 사용할 수 있습니다. 이 절의 컨텍스트에서 DEFAULT는 키워드가 아니므로 식별자로 구분해야 합니다. 파일 그룹을 지정하지 않으면 큐는 데이터베이스의 기본 파일 그룹을 사용합니다.

## <a name="remarks"></a>설명

큐는 SELECT 문의 대상이 될 수 있습니다. 그러나 큐의 내용은 SEND, RECEIVE, END CONVERSATION 등 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화에서 실행되는 문을 사용해야만 수정할 수 있습니다. 큐는 INSERT, UPDATE, DELETE 또는 TRUNCATE 문의 대상이 될 수 없습니다.

큐는 임시 개체일 수 없습니다. 따라서 **#** 으로 시작하는 큐 이름은 유효하지 않습니다.

비활성 상태의 큐를 만들면 큐에서 메시지를 받기 전까지 서비스를 위한 해당 인프라를 사용할 수 있습니다.

큐에 메시지가 없어도 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 활성화 저장 프로시저를 중지하지 않습니다. 잠시 동안이라도 큐에 메시지가 없을 경우 활성화 저장 프로시저가 종료됩니다.

큐를 만들 때가 아니라 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 저장 프로시저를 시작할 때 활성화 저장 프로시저에 대한 권한이 검사됩니다. CREATE QUEUE 문은 EXECUTE AS 절에 지정된 사용자에게 PROCEDURE NAME 절에 지정된 저장 프로시저를 실행할 수 있는 권한이 있는지 확인하지 않습니다.

큐를 사용할 수 없는 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 데이터베이스 전송 큐에서 큐를 사용하는 서비스에 대한 메시지를 보유합니다. sys.transmission_queue 카탈로그 뷰에서는 전송 큐 보기를 제공합니다.

큐는 스키마가 소유한 개체입니다. 따라서 큐는 sys.objects 카탈로그 뷰에 표시됩니다.

다음 표에서는 큐의 열을 나열합니다.

|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|
|상태|**tinyint**|메시지의 상태입니다. RECEIVE 문은 상태가 **1**인 모든 메시지를 반환합니다. 메시지 보존이 설정되면 상태는 0으로 설정됩니다. 메시지 보존이 설정되지 않으면 메시지는 큐에서 삭제됩니다. 큐의 메시지는 다음 값 중 하나를 포함할 수 있습니다.<br /><br /> **0**=보존된 받은 메시지<br /><br /> **1**=수신 준비 완료<br /><br /> **2**=아직 완료되지 않음ㄴ<br /><br /> **3**=보존된 보낸 메시지|
|priority|**tinyint**|이 메시지에 할당된 우선 순위 수준입니다.|
|queuing_order|**bigint**|큐 내의 메시지 정렬 번호입니다.|
|conversation_group_id|**uniqueidentifier**|이 메시지가 속하는 대화 그룹의 식별자입니다.|
|conversation_handle|**uniqueidentifier**|이 메시지가 속하는 대화의 핸들입니다.|
|message_sequence_number|**bigint**|대화 내의 메시지 시퀀스 번호입니다.|
|service_name|**nvarchar(512)**|대화와 연관된 서비스의 이름입니다.|
|service_id|**int**|대화와 연관된 서비스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 식별자입니다.|
|service_contract_name|**nvarchar(256)**|대화에서 준수하는 계약의 이름입니다.|
|service_contract_id|**int**|대화에서 준수하는 계약의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 식별자입니다.|
|message_type_name|**nvarchar(256)**|메시지를 설명하는 메시지 유형의 이름입니다.|
|message_type_id|**int**|메시지를 설명하는 메시지 유형의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 식별자입니다.|
|validation|**nchar(2)**|메시지에 사용된 유효성 검사입니다.<br /><br /> E=비어 있음<br /><br /> N=없음<br /><br /> X=XML|
|message_body|**varbinary(max)**|메시지 내용입니다.|
|message_id|**uniqueidentifier**|메시지의 고유 식별자입니다.|

## <a name="permissions"></a>사용 권한

큐를 만들 수 있는 권한은 `db_ddladmin`, `db_owner` 고정 데이터베이스 역할 및 `sysadmin` 고정 서버 역할의 멤버를 사용합니다.

큐에 대한 `REFERENCES` 권한은 기본적으로 큐의 소유자, `db_ddladmin`, `db_owner` 고정 데이터베이스 역할의 멤버 또는 `sysadmin` 고정 서버 역할의 멤버로 설정됩니다.

큐에 대한 `RECEIVE` 권한은 기본적으로 큐의 소유자, `db_owner` 고정 데이터베이스 역할의 멤버 또는 `sysadmin` 고정 서버 역할의 멤버로 설정됩니다.

## <a name="examples"></a>예

### <a name="a-creating-a-queue-with-no-parameters"></a>A. 매개 변수 없이 큐 만들기

다음 예에서는 메시지를 받을 수 있는 큐를 만듭니다. 큐에 대해 지정된 활성화 저장 프로시저가 없습니다.

```sql
CREATE QUEUE ExpenseQueue ;
```

### <a name="b-creating-an-unavailable-queue"></a>B. 사용할 수 없는 큐 만들기

다음 예에서는 메시지를 받을 수 없는 큐를 만듭니다. 큐에 대해 지정된 활성화 저장 프로시저가 없습니다.

```sql
CREATE QUEUE ExpenseQueue WITH STATUS=OFF ;
```

### <a name="c-creating-a-queue-and-specify-internal-activation-information"></a>C. 큐 만들기 및 내부 활성화 정보 지정

다음 예에서는 메시지를 받을 수 있는 큐를 만듭니다. 큐에서 메시지를 받으면 큐가 `expense_procedure` 저장 프로시저를 시작합니다. 이 저장 프로시저는 `ExpenseUser` 사용자로 실행됩니다. 큐는 최대 `5`개의 저장 프로시저 인스턴스를 시작합니다.

```sql
CREATE QUEUE ExpenseQueue
    WITH STATUS=ON,
    ACTIVATION (
        PROCEDURE_NAME = expense_procedure
        , MAX_QUEUE_READERS = 5
        , EXECUTE AS 'ExpenseUser' ) ;
```

### <a name="d-creating-a-queue-on-a-specific-filegroup"></a>D. 특정 파일 그룹에 큐 만들기

다음 예에서는 `ExpenseWorkFileGroup` 파일 그룹에 큐를 만듭니다.

```sql
CREATE QUEUE ExpenseQueue
    ON ExpenseWorkFileGroup ;
```

### <a name="e-creating-a-queue-with-multiple-parameters"></a>E. 여러 매개 변수로 큐 만들기

다음 예에서는 `DEFAULT` 파일 그룹에 큐를 만듭니다. 이 큐는 사용할 수 없습니다. 메시지가 속한 대화가 끝날 때까지 이 큐에 메시지가 보관됩니다. ALTER QUEUE를 사용하여 큐를 사용할 수 있게 설정하면 큐가 `2008R2.dbo.expense_procedure` 저장 프로시저를 시작하여 메시지를 처리합니다. 이 저장 프로시저는 `CREATE QUEUE` 문을 실행한 사용자로 실행됩니다. 큐는 최대 `10`개의 저장 프로시저 인스턴스를 시작합니다.

```sql
CREATE QUEUE ExpenseQueue
    WITH STATUS = OFF
      , RETENTION = ON
      , ACTIVATION (
          PROCEDURE_NAME = AdventureWorks2012.dbo.expense_procedure
          , MAX_QUEUE_READERS = 10
          , EXECUTE AS SELF )
    ON [DEFAULT];
```

## <a name="see-also"></a>참고 항목

- [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)
- [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)
- [DROP QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)
- [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)
- [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
