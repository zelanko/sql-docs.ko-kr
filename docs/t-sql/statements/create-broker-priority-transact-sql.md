---
description: CREATE BROKER PRIORITY(Transact-SQL)
title: CREATE BROKER PRIORITY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE BROKER PRIORITY
- PRIORITY_TSQL
- CREATE_BROKER_PRIORITY_TSQL
- PRIORITY
- CREATE BROKER
- BROKER_TSQL
- BROKER
- CREATE_BROKER_TSQL
- BROKER PRIORITY
- BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE BROKER PRIORITY statement
ms.assetid: e0bbebfa-b7c3-4825-8169-7281f7e6de98
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c753f9dc977f94064161ee340ebced685dd9f6c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478985"
---
# <a name="create-broker-priority-transact-sql"></a>CREATE BROKER PRIORITY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  우선 순위 수준을 정의하고 우선 순위 수준을 할당할 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화를 결정하기 위한 조건 집합을 설정합니다. 우선 순위 수준은 대화 우선 순위에 지정된 계약 및 서비스 조합과 동일한 조합을 사용하는 모든 대화 엔드포인트에 할당됩니다. 우선 순위 값의 범위는 1(낮음)에서 10(높음) 사이입니다. 기본값은 5입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
CREATE BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
[ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = {PriorityValue | DEFAULT } ]  
       )  
]  
[;]  
  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *ConversationPriorityName*  
 이 대화 우선 순위의 이름을 지정합니다. 이름은 현재 데이터베이스에서 고유해야 하며 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 SET  
 대화 우선 순위를 대화에 적용할지 여부를 결정하는 조건을 지정합니다. 지정된 경우 SET이 CONTRACT_NAME, LOCAL_SERVICE_NAME, REMOTE_SERVICE_NAME 또는 PRIORITY_LEVEL 조건을 하나 이상 포함해야 합니다. SET이 지정되지 않은 경우 세 조건 모두에 대한 기본값이 설정됩니다.  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 대화 우선 순위를 대화에 적용할지 여부를 결정하기 위한 조건으로 사용할 계약 이름을 지정합니다. *ContractName*은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 식별자이며 현재 데이터베이스의 계약 이름을 지정해야 합니다.  
  
 *ContractName*  
 대화를 시작한 BEGIN DIALOG 문에 ON CONTRACT *ContractName*이 지정된 대화에만 대화 우선 순위가 적용될 수 있도록 지정합니다.  
  
 ANY  
 사용하는 계약에 관계없이 모든 대화에 대화 우선 순위가 적용될 수 있도록 지정합니다.  
  
 기본값은 ANY입니다.  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 대화 엔드포인트에 대화 우선 순위를 적용할지 여부를 결정하는 조건으로 사용될 서비스 이름을 지정합니다.  
  
 *LocalServiceName*은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 식별자입니다. 현재 데이터베이스에 있는 서비스의 이름을 지정해야 합니다.  
  
 *LocalServiceName*  
 대화 우선 순위가 다음 항목에 적용될 수 있도록 지정합니다.  
  
-   시작자 서비스 이름이 *LocalServiceName*과 일치하는 모든 시작자 대화 엔드포인트입니다.  
  
-   대상 서비스 이름이 *LocalServiceName*과 일치하는 모든 대상 대화 엔드포인트입니다.  
  
 ANY  
 -   엔드포인트에서 사용하는 로컬 서비스 이름에 관계없이 모든 대화 엔드포인트에 대화 우선 순위가 적용될 수 있도록 지정합니다.  
  
 기본값은 ANY입니다.  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 대화 엔드포인트에 대화 우선 순위를 적용할지 여부를 결정하는 조건으로 사용될 서비스 이름을 지정합니다.  
  
 *RemoteServiceName*은 **nvarchar(256)** 형식의 리터럴입니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 바이트 단위로 비교하여 일치하는 *RemoteServiceName*를 찾습니다. 비교 시 대/소문자가 구분되고 현재 데이터 정렬은 고려되지 않습니다. 대상 서비스는 현재 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 또는 원격 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 있을 수 있습니다.  
  
 '*RemoteServiceName*'  
 대화 우선 순위가 다음 항목에 적용될 수 있도록 지정합니다.  
  
-   연결된 대상 서비스 이름이 *RemoteServiceName*과 일치하는 모든 시작자 대화 엔드포인트입니다.  
  
-   연결된 시작 서비스 이름이 *RemoteServiceName*과 일치하는 모든 대상 대화 엔드포인트입니다.  
  
 ANY  
 엔드포인트와 연결된 원격 서비스 이름에 관계없이 모든 대화 엔드포인트에 대화 우선 순위가 적용되도록 지정합니다.  
  
 기본값은 ANY입니다.  
  
 PRIORITY_LEVEL = { *PriorityValue* | **DEFAULT** }  
 대화 우선 순위에 지정된 계약 및 서비스를 사용하는 모든 대화 엔드포인트에 할당할 우선 순위를 지정합니다. *PriorityValue*는 1(가장 낮은 우선 순위)에서 10(가장 높은 우선 순위) 사이의 정수 리터럴이어야 합니다. 기본값은 5입니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 대화 엔드포인트에 우선 순위 수준을 할당합니다. 우선 순위 수준은 엔드포인트와 연관된 작업의 우선 순위를 제어합니다. 각 대화에는 두 개의 대화 엔드포인트가 있습니다.  
  
-   시작자 대화 엔드포인트는 대화의 한 쪽을 시작자 서비스 및 시작자 큐와 연결합니다. 시작자 대화 엔드포인트는 BEGIN DIALOG 문이 실행될 때 생성됩니다. 시작자 대화 엔드포인트와 연관된 작업에는 다음이 포함됩니다.  
  
    -   시작자 서비스에서 보내기  
  
    -   시작자 큐에서 받기  
  
    -   시작자 큐에서 다음 대화 그룹 가져오기  
  
-   대상 대화 엔드포인트는 대화의 다른 한 쪽을 대상 서비스 및 큐와 연결합니다. 대상 대화 엔드포인트는 대화를 사용하여 대상 큐에 메시지를 보낼 때 생성됩니다. 대상 대화 엔드포인트와 연관된 작업에는 다음이 포함됩니다.  
  
    -   대상 큐에서 받기  
  
    -   대상 서비스에서 보내기  
  
    -   대상 큐에서 다음 대화 그룹 가져오기  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 대화 엔드포인트가 생성될 때 대화 우선 순위 수준을 할당합니다. 대화 엔드포인트는 대화가 종료될 때까지 우선 순위 수준을 그대로 유지합니다. 새 우선 순위 또는 기존 우선 순위의 변경 사항은 기존 대화에 적용되지 않습니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 계약 및 서비스 조건이 엔드포인트의 속성에 가장 일치하는 대화 우선 순위의 우선 순위 수준을 대화 엔드포인트에 할당합니다. 다음 표에서는 일치 우선 순위를 보여 줍니다.  
  
|작업 계약|작업 로컬 서비스|작업 원격 서비스|  
|------------------------|-----------------------------|------------------------------|  
|*ContractName*|*LocalServiceName*|*RemoteServiceName*|  
|*ContractName*|*LocalServiceName*|ANY|  
|*ContractName*|ANY|*RemoteServiceName*|  
|*ContractName*|ANY|ANY|  
|ANY|*LocalServiceName*|*RemoteServiceName*|  
|ANY|*LocalServiceName*|ANY|  
|ANY|ANY|*RemoteServiceName*|  
|ANY|ANY|ANY|  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 먼저 지정된 계약, 로컬 서비스 및 원격 서비스가 작업에 사용된 것과 일치하는 우선 순위를 찾습니다. 이러한 우선 순위를 찾지 못한 경우에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]은 작업에 사용된 것과 일치하는 계약 및 로컬 서비스가 있고 원격 서비스가 ANY로 지정된 우선 순위를 찾습니다. 이는 우선 순위 표에 나열된 다양한 우선 순위 모두에 대해 계속 수행됩니다. 일치하는 항목이 발견되지 않으면 해당 작업에 기본 우선 순위 5가 할당됩니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 대화 엔드포인트마다 개별적으로 우선 순위 수준을 할당합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 시작자와 대상 대화 엔드포인트 모두에 우선 순위 수준을 할당하도록 하려면 두 엔드포인트에 대화 우선 순위가 적용되는지 확인해야 합니다. 시작자 대화 엔드포인트와 대상 대화 엔드포인트가 각기 다른 데이터베이스에 있는 경우 각 데이터베이스에 대화 우선 순위를 만들어야 합니다. 대화의 두 대화 엔드포인트에는 일반적으로 동일한 우선 순위 수준이 지정되지만 다른 우선 순위를 지정할 수도 있습니다.  
  
 큐에서 메시지나 대화 그룹 식별자를 수신하는 작업에는 항상 우선 순위 수준이 적용됩니다. 우선 순위 수준은 또한 한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 다른 인스턴스로 메시지를 전송할 때도 적용됩니다.  
  
 다음과 같이 메시지를 전송할 때는 우선 순위 수준이 사용되지 않습니다.  
  
-   HONOR_BROKER_PRIORITY 데이터베이스 옵션이 OFF로 설정된 데이터베이스에서 전송하는 경우. 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
-   동일한 Database Engine 인스턴스의 서비스 간에 전송하는 경우  
  
-   데이터베이스에 대화 우선 순위가 생성되어 있지 않은 경우에는 데이터베이스의 모든 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 작업에 기본 우선 순위 5가 할당됩니다.  
  
## <a name="permissions"></a>사용 권한  
 대화 우선 순위를 만들 수 있는 권한은 기본적으로 db_ddladmin 또는 db_owner 고정 데이터베이스 역할 및 sysadmin 고정 서버 역할의 멤버에게 있습니다. 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-assigning-a-priority-level-to-both-directions-of-a-conversation"></a>A. 대화의 양쪽 방향에 우선 순위 수준 할당  
 다음 두 대화 우선 순위는 `SimpleContract`와 `TargetService` 사이에서 `InitiatorAService`를 사용하는 모든 작업에 우선 순위 수준 3을 할당합니다.  
  
```  
CREATE BROKER PRIORITY InitiatorAToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = InitiatorServiceA,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 3);  
CREATE BROKER PRIORITY TargetToInitiatorAPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceA',  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-setting-the-priority-level-for-all-conversations-that-use-a-contract"></a>B. 계약을 사용하는 모든 대화의 우선 순위 수준 설정  
 `7`라는 계약을 사용하는 모든 작업에 우선 순위 수준 `SimpleContract`을 할당합니다. 이 경우 `SimpleContract`와 로컬 또는 원격 서비스를 모두 지정하는 다른 우선 순위가 없다고 가정합니다.  
  
```  
CREATE BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 7);  
```  
  
### <a name="c-setting-a-base-priority-level-for-a-database"></a>C. 데이터베이스의 기본 우선 순위 수준 설정  
 두 특정 서비스의 대화 우선 순위를 정의한 다음 다른 모든 대화 엔드포인트와 일치하는 대화 우선 순위를 정의합니다. 이는 항상 5인 기본 우선 순위를 대체하지 않지만 기본값이 할당되는 항목 수를 최소화합니다.  
  
```  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ClaimPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 9);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ApprovalPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/BasePriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="d-creating-three-priority-levels-for-a-target-service-by-using-services"></a>D. 서비스를 사용하여 대상 서비스의 세 가지 우선 순위 수준 만들기  
 세 가지 성능 수준인 금(높음), 은(중간), 동(낮음)을 제공하는 시스템을 지원합니다. 계약은 하나지만 각 수준마다 별도의 시작자 서비스가 있습니다. 모든 시작자 서비스는 중앙 대상 서비스와 통신합니다.  
  
```sql  
CREATE BROKER PRIORITY GoldInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = GoldInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY GoldTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'GoldInitiatorService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = SilverInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY SilverTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'SilverInitiatorService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzeInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = BronzeInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 2);  
CREATE BROKER PRIORITY BronzeTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'BronzeInitiatorService',  
         PRIORITY_LEVEL = 2);  
```  
  
### <a name="e-creating-three-priority-levels-for-multiple-services-using-contracts"></a>E. 계약을 사용하여 여러 서비스의 세 가지 우선 순위 수준 만들기  
 세 가지 성능 수준인 금(높음), 은(중간), 동(낮음)을 제공하는 시스템을 지원합니다. 각 수준은 별도의 계약을 가집니다. 이러한 우선 순위는 해당 계약을 사용하는 대화에서 참조하는 모든 서비스에 적용됩니다.  
  
```sql  
CREATE BROKER PRIORITY GoldPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = GoldContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SilverContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzePriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = BronzeContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 2);  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION&#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [CREATE CONTRACT&#40;Transact-SQL&#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE&#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [GET CONVERSATION GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)   
 [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md)   
 [sys.conversation_priorities&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
