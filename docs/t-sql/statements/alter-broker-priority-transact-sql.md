---
title: ALTER BROKER PRIORITY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_BROKER_TSQL
- ALTER BROKER PRIORITY
- ALTER BROKER
- ALTER_BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER BROKER PRIORITY statement
- ssbdiagnose
ms.assetid: 15fda1b2-e4dd-4f9d-935a-2e38926075b2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5ccaa708ec41319c8eaf17c1f917d940a086fb62
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895712"
---
# <a name="alter-broker-priority-transact-sql"></a>ALTER BROKER PRIORITY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 우선 순위의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
ALTER BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
{ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = { PriorityValue | DEFAULT } ]  
              )  
}  
[;]  
  
```  
  
## <a name="arguments"></a>인수  
 *ConversationPriorityName*  
 변경할 대화 우선 순위의 이름을 지정합니다. 현재 데이터베이스의 대화 우선 순위를 참조하는 이름이어야 합니다.  
  
 SET  
 대화 우선 순위를 대화에 적용할지 여부를 결정하는 조건을 지정합니다. SET은 필수이며 CONTRACT_NAME, LOCAL_SERVICE_NAME, REMOTE_SERVICE_NAME 또는 PRIORITY_LEVEL 조건을 하나 이상 포함해야 합니다.  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 대화 우선 순위를 대화에 적용할지 여부를 결정하기 위한 조건으로 사용할 계약 이름을 지정합니다. *ContractName*은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 식별자이며 현재 데이터베이스의 계약 이름을 지정해야 합니다.  
  
 *ContractName*  
 대화를 시작한 BEGIN DIALOG 문에 ON CONTRACT *ContractName*이 지정된 대화에만 대화 우선 순위가 적용될 수 있도록 지정합니다.  
  
 ANY  
 사용하는 계약에 관계없이 모든 대화에 대화 우선 순위가 적용될 수 있도록 지정합니다.  
  
 CONTRACT_NAME을 지정하지 않으면 대화 우선 순위의 계약 속성이 변경되지 않습니다.  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 대화 엔드포인트에 대화 우선 순위를 적용할지 여부를 결정하는 조건으로 사용될 서비스 이름을 지정합니다.  
  
 *LocalServiceName*은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 식별자이며 현재 데이터베이스에 있는 서비스의 이름을 지정해야 합니다.  
  
 *LocalServiceName*  
 대화 우선 순위가 다음 항목에 적용될 수 있도록 지정합니다.  
  
-   시작자 서비스 이름이 *LocalServiceName*과 일치하는 모든 시작자 대화 엔드포인트입니다.  
  
-   대상 서비스 이름이 *LocalServiceName*과 일치하는 모든 대상 대화 엔드포인트입니다.  
  
 ANY  
 -   엔드포인트에서 사용하는 로컬 서비스 이름에 관계없이 모든 대화 엔드포인트에 대화 우선 순위가 적용될 수 있도록 지정합니다.  
  
 LOCAL_SERVICE_NAME을 지정하지 않으면 대화 우선 순위의 로컬 서비스 속성이 변경되지 않습니다.  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 대화 엔드포인트에 대화 우선 순위를 적용할지 여부를 결정하는 조건으로 사용될 서비스 이름을 지정합니다.  
  
 *RemoteServiceName*은 **nvarchar(256)** 형식의 리터럴입니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 바이트 단위로 비교하여 일치하는 *RemoteServiceName*를 찾습니다. 비교 시 대/소문자가 구분되고 현재 데이터 정렬은 고려되지 않습니다. 대상 서비스는 현재 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 또는 원격 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 있을 수 있습니다.  
  
 '*RemoteServiceName*'  
 대화 우선 순위가 다음 항목에 적용되도록 지정합니다.  
  
-   연결된 대상 서비스 이름이 *RemoteServiceName*과 일치하는 모든 시작자 대화 엔드포인트입니다.  
  
-   연결된 시작 서비스 이름이 *RemoteServiceName*과 일치하는 모든 대상 대화 엔드포인트입니다.  
  
 ANY  
 엔드포인트와 연결된 원격 서비스 이름에 관계없이 모든 대화 엔드포인트에 대화 우선 순위가 적용되도록 지정합니다.  
  
 REMOTE_SERVICE_NAME을 지정하지 않으면 대화 우선 순위의 원격 서비스 속성이 변경되지 않습니다.  
  
 PRIORITY_LEVEL = { *PriorityValue* | **DEFAULT** }  
 대화 우선 순위에 지정된 계약 및 서비스를 사용하는 모든 대화 엔드포인트에 할당할 우선 순위 수준을 지정합니다. *PriorityValue*는 1(가장 낮은 우선 순위)에서 10(가장 높은 우선 순위) 사이의 정수 리터럴이어야 합니다.  
  
 PRIORITY_LEVEL을 지정하지 않으면 대화 우선 순위의 우선 순위 수준 속성이 변경되지 않습니다.  
  
## <a name="remarks"></a>설명  
 ALTER BROKER PRIORITY를 사용하여 변경한 속성은 기존 대화에 적용되지 않습니다. 기존 대화에는 대화가 시작될 때 할당된 우선 순위가 계속 적용됩니다.  
  
 자세한 내용은 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 대화 우선 순위를 만들 수 있는 권한은 기본적으로 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할 및 **sysadmin** 고정 서버 역할의 멤버에게 있습니다. 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-only-the-priority-level-of-an-existing-conversation-priority"></a>A. 기존 대화 우선 순위의 우선 순위 수준만 변경  
 우선 순위 수준을 변경하지만 계약, 로컬 서비스 또는 원격 서비스 속성은 변경하지 않습니다.  
  
```  
ALTER BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-changing-all-of-the-properties-of-an-existing-conversation-priority"></a>B. 기존 대화 우선 순위의 모든 속성 변경  
 우선 순위 수준, 계약, 로컬 서비스 및 원격 서비스 속성을 변경합니다.  
  
```  
ALTER BROKER PRIORITY SimpleContractPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContractB,  
         LOCAL_SERVICE_NAME = TargetServiceB,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceB',  
         PRIORITY_LEVEL = 8);  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE BROKER PRIORITY&#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.conversation_priorities&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
