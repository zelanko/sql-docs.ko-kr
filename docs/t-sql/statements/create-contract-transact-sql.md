---
title: "계약 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONTRACT_TSQL
- CREATE_CONTRACT_TSQL
- CREATE CONTRACT
- CONTRACT
dev_langs: TSQL
helpviewer_keywords:
- CREATE CONTRACT statement
- contracts [Service Broker], creating
- message types [Service Broker], contracts
ms.assetid: 494cbfa6-8e93-4161-a64d-90d681915211
caps.latest.revision: "48"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26a8d2c2826e091322a1cec35d6ffe1d9ca379e0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-contract-transact-sql"></a>CREATE CONTRACT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 계약을 만듭니다. 계약은 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화에 사용되는 메시지 유형을 정의하며 해당 유형의 메시지를 보낼 수 있는 대화 상대도 결정합니다. 각 대화는 계약을 따릅니다. 시작 서비스는 대화가 시작될 때 대화에 대한 계약을 지정합니다. 대상 서비스는 대상 서비스가 받아들이는 대화에 대한 계약을 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE CONTRACT contract_name  
   [ AUTHORIZATION owner_name ]  
      (  {   { message_type_name | [ DEFAULT ] }  
          SENT BY { INITIATOR | TARGET | ANY }   
       } [ ,...n] )   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *contract_name*  
 만들 계약의 이름입니다. 새 계약은 현재 데이터베이스에 생성되고 AUTHORIZATION 절에서 지정한 보안 주체가 소유합니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다. *contract_name* 최대 128 자를 사용할 수 있습니다.  
  
> [!NOTE]  
>  만들지 마십시오 키워드를 사용 하는 계약에 대 한 모든는 *contract_name*합니다. CREATE BROKER PRIORITY에서 계약 이름에 ANY를 지정하면 모든 계약에 대해 우선 순위가 고려됩니다. 이러한 규칙은 이름이 ANY인 계약으로 제한되지 않습니다.  
  
 권한 부여 *owner_name*  
 지정한 데이터베이스 사용자 또는 역할로 계약의 소유자를 설정합니다. 현재 사용자가 **dbo** 또는 **sa**, *owner_name* 유효한 사용자 또는 역할의 이름일 수 있습니다. 그렇지 않으면 *owner_name* 현재 사용자의 이름, 현재 사용자가을 대 한 권한을 가장 한 사용자의 이름 또는 현재 사용자가 속해 있는 역할의 이름 이어야 합니다. 이 절을 생략하면 계약이 현재 사용자에 속합니다.  
  
 *message_type_name*  
 계약의 일부로 포함될 메시지 유형의 이름입니다.  
  
 SENT BY  
 지정된 메시지 유형의 메시지를 보낼 수 있는 끝점을 지정합니다. 계약은 서비스에서 특정 대화를 소유하기 위해 사용할 수 있는 메시지를 문서화합니다. 각 대화는 두 개의 끝점:는 *초기자* 대화를 시작한 서비스, 끝점 및 *대상* 끝점, 서비스는 시작 자가 연결입니다.  
  
 INITIATOR  
 대화의 시작자만 지정된 메시지 유형의 메시지를 보낼 수 있음을 나타냅니다. 대화를 시작 하는 서비스 라고는 *초기자* 대화의 합니다.  
  
 TARGET  
 대화의 대상만 지정된 메시지 유형의 메시지를 보낼 수 있음을 나타냅니다. 다른 서비스에 의해 시작 된 대화를 수락 하는 서비스 라고는 *대상* 대화의 합니다.  
  
 ANY  
 시작자와 대상 모두 이 유형의 메시지를 보낼 수 있음을 나타냅니다.  
  
 [DEFAULT]  
 이 계약에서 기본 메시지 유형의 메시지를 지원함을 나타냅니다. 기본적으로 모든 데이터베이스에는 DEFAULT라는 메시지 유형이 있습니다. 이 메시지 유형은 유효성 검사 NONE을 사용합니다. 이 절의 컨텍스트에서 DEFAULT는 키워드가 아니므로 식별자로 구분해야 합니다. Microsoft SQL Server에서는 DEFAULT 메시지 유형을 지정하는 DEFAULT 계약도 제공합니다.  
  
## <a name="remarks"></a>주의  
 계약에서 메시지 유형의 순서는 중요하지 않습니다. 대상이 첫 번째 메시지를 받으면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 대화 상대 중 어느 한 쪽이 언제든지 해당 대화 상대에 허용된 메시지를 보낼 수 있도록 허용합니다. 예를 들어 대화의 시작자는 메시지 유형을 보낼 수 **//Adventure-Works.com/Expenses/SubmitExpense**, [!INCLUDE[ssSB](../../includes/sssb-md.md)] 개수에 관계 없이 보낼 수 있도록 허용 **SubmitExpense**중 대화의 메시지입니다.  
  
 계약에서 메시지 유형과 방향은 변경할 수 없습니다. 계약에 대한 AUTHORIZATION을 변경하려면 ALTER AUTHORIZATION 문을 사용합니다.  
  
 계약은 시작자가 메시지를 보낼 수 있도록 허용해야 합니다. 계약이 하나 이상의 메시지 유형(SENT BY ANY 또는 SENT BY INITIATOR)을 포함하지 않으면 CREATE CONTRACT 문이 실패합니다.  
  
 계약에 관계 없이 서비스 메시지 유형을 받습니다 항상 수 `http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`, `http://schemas.microsoft.com/SQL/ServiceBroker/Error`, 및 `http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog`합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 응용 프로그램에 대한 시스템 메시지에 이러한 메시지 유형을 사용합니다.  
  
 계약은 임시 개체가 아닐 수 있습니다. #로 시작하는 계약 이름은 허용되지만 영구 개체입니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로의 멤버는 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할 및 **sysadmin** 고정된 서버 역할 계약을 만들 수 있습니다.  
  
 기본적으로 멤버의 계약의 소유자는 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버는 **sysadmin** 고정된 서버 역할에 대 한 참조는 계약에 대 한 권한이 있습니다.  
  
 CREATE CONTRACT 문을 실행하는 사용자에게는 지정된 모든 메시지 유형에 대한 REFERENCES 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 **A. 계약 만들기**  
  
 다음 예에서는 세 메시지 유형을 기반으로 경비 변제 계약을 만듭니다.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE           
    [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
    VALIDATION= WELL_FORMED_XML ;           
  
CREATE CONTRACT            
    [//Adventure-Works.com/Expenses/ExpenseSubmission]           
    ( [//Adventure-Works.com/Expenses/SubmitExpense]           
          SENT BY INITIATOR,           
      [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
          SENT BY TARGET,           
      [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
          SENT BY TARGET           
    ) ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [계약 삭제 &#40; Transact SQL &#41;](../../t-sql/statements/drop-contract-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
