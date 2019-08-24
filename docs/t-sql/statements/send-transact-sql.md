---
title: SEND(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SEND_ON_CONVERSATION_TSQL
- ON_CONVERSATION_TSQL
- SEND
- SEND_TSQL
- SEND ON CONVERSATION
- ON CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], message sending
- SEND statement
- messages [Service Broker], sending
- sending messages
ms.assetid: b6e66aeb-1714-4c2b-b7c2-d386d77b0d46
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: af65ac5257da6bc04a5a33649007ae849366e10c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913902"
---
# <a name="send-transact-sql"></a>SEND(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

하나 이상의 기존 대화를 사용하여 메시지를 보냅니다.  
  
![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
ON CONVERSATION *conversation_handle [.. @conversation_handle_n]*  
메시지가 속해 있는 대화를 지정합니다. *conversation_handle*은 유효한 대화 식별자가 있어야 합니다. 같은 대화 핸들을 두 번 이상 사용할 수 없습니다.  
  
MESSAGE TYPE *message_type_name*  
보낸 메시지의 메시지 유형을 지정합니다. 이 메시지 유형은 이 대화에 사용된 서비스 계약에 포함되어야 합니다. 이 계약은 대화의 이 쪽에서 보내는 메시지 유형을 허용해야 합니다. 예를 들어 대화의 대상 서비스는 계약에 SENT BY TARGET 또는 SENT BY ANY로 지정되어 있는 메시지만 보낼 수 있습니다. 이 절이 생략된 경우 메시지 유형은 DEFAULT입니다.  
  
*message_body_expression*  
메시지 본문을 나타내는 식을 제공합니다. *message_body_expression*은 선택 사항입니다. 하지만 *message_body_expression*이 있으면 해당 식은 **varbinary(max)** 로 변환될 수 있는 유형이어야 합니다. 식은 NULL일 수 없습니다. 이 절이 생략된 경우에는 메시지 본문이 비어 있습니다.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  SEND 문이 일괄 처리 또는 저장 프로시저에서 첫 번째 문이 아닌 경우 이전 문은 세미콜론(;)으로 종료되어야 합니다.  
  
SEND 문은 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 하나 이상의 한쪽 끝에 있는 서비스에서 이 대화의 다른 쪽 끝에 있는 서비스로 메시지를 전송합니다. 그런 다음 RECEIVE 문이 대상 서비스와 연결된 큐에서 전송된 메시지를 검색합니다.  
  
ON CONVERSATION 절에 제공되는 대화 핸들은 다음의 세 가지 원본 중 하나에서 나옵니다.  
  
- 전송된 메시지가 다른 서비스에서 수신한 메시지에 응답하지 않는 경우에는 대화를 만든 BEGIN DIALOG 문에서 반환된 대화 핸들을 사용합니다.  
  
- 전송된 메시지가 다른 서비스에서 이전에 수신한 메시지에 응답하지 않는 경우에는 원본 메시지를 반환한 RECEIVE 문에서 반환된 대화 핸들을 사용합니다.  
  
- 경우에 따라 SEND 문을 포함하는 코드와 대화 핸들을 제공하는 BEGIN DIALOG 또는 RECEIVE 문을 포함하는 코드는 별개입니다. 이 경우 대화 핸들은 SEND 문을 포함하는 코드에 전달된 상태 정보의 데이터 항목 중 하나여야 합니다.  
  
다른 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 서비스로 전송되는 메시지는 원격 인스턴스의 서비스 큐로 전송되기 전까지 현재 데이터베이스의 전송 큐에 저장됩니다. 동일한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 서비스로 전송되는 메시지는 이 서비스와 연결된 큐에 직접 보관됩니다. 특정 상황으로 인해 로컬 메시지를 대상 서비스 큐로 직접 이동할 수 없는 경우 문제가 해결될 때까지 전송 큐에 저장할 수 있습니다. 이 문제의 예로는 몇 가지 오류 유형 또는 비활성 상태의 대상 서비스 큐가 포함됩니다. **sys.transmission_queue** 시스템 뷰를 사용하면 전송 큐에 있는 메시지를 확인할 수 있습니다.  
  
SEND는 원자성 문입니다. SEND 문이 여러 대화에서 메시지를 보내고 대화의 오류 상태 등을 이유로 해당 문이 실패할 경우 메시지가 전송 큐에 저장되지 않거나 대상 서비스 큐에 보관되지 않습니다.  
  
Service Broker는 같은 SEND 문의 여러 대화에서 전송된 메시지의 스토리지 및 전송을 최적화합니다.  
  
인스턴스에 대한 전송 큐에 있는 메시지는 다음을 기반으로 하여 순서대로 전송됩니다.  
  
- 연결된 대화 엔드포인트의 우선 순위 수준  
  
- 우선 순위 수준 내에서 대화에 있는 해당 메시지의 보내기 순서  
  
대화 우선 순위에 지정된 우선 순위 수준은 HONOR_BROKER_PRIORITY 데이터베이스 옵션이 ON으로 설정된 경우에만 전송 큐의 메시지에 적용됩니다. HONOR_BROKER_PRIORITY 옵션이 OFF로 설정되면 해당 데이터베이스에 대한 전송 큐의 모든 메시지에 기본 우선 순위 수준 5가 할당됩니다. 메시지가 동일한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 서비스 큐에 직접 삽입되는 SEND에는 우선 순위 수준이 적용되지 않습니다.  
  
SEND 문은 대화당 요청된 배달을 확인하기 위해 메시지가 전송되는 각 대화를 별도로 잠급니다.  
  
SEND는 사용자 정의 함수에 유효하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
메시지를 보내려면 현재 사용자가 메시지를 보내는 모든 서비스의 큐에 대한 RECEIVE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 대화를 시작하고 해당 대화에서 XML 메시지를 보냅니다. 메시지를 보내기 위해 이 예제에서는 xml 개체를 **varbinary(max)** 로 변환합니다.  
  
```sql
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ExpenseReport XML ;  
  
SET @ExpenseReport = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle  
FROM SERVICE [//Adventure-Works.com/Expenses/ExpenseClient]  
TO SERVICE '//Adventure-Works.com/Expenses'  
ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing] ;  
  
SEND ON CONVERSATION @dialog_handle  
    MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense]  
    (@ExpenseReport) ;  
```  
  
다음 예에서는 세 개의 대화를 시작하고 각 대화에서 XML 메시지를 보냅니다.  
  
```sql
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
SEND ON CONVERSATION (@dialog_handle1, @dialog_handle2, @dialog_handle3)  
    MESSAGE TYPE [//AllDBs/OrderMsg]  
    (@OrderMsg) ;  
```  
  
## <a name="see-also"></a>참고 항목  
[BEGIN DIALOG CONVERSATION&#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
[END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
[RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)   
[sys.transmission_queue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  
