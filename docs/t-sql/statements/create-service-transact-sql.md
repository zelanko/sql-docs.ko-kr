---
title: "서비스 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SERVICE_TSQL
- SERVICE
- CREATE SERVICE
- SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- services [Service Broker], creating
- CREATE SERVICE statement
- contracts [Service Broker], service creation
ms.assetid: fb804fa2-48eb-4878-a12f-4e0d5f4bc9e3
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f281cd0f60c0f4f2a37419af4870d927868183a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-service-transact-sql"></a>CREATE SERVICE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 서비스를 만듭니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스는 특정 태스크나 작업 집합의 이름입니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 이 서비스 이름을 사용하여 메시지를 라우팅하고 데이터베이스 내의 올바른 큐에 메시지를 전달하고 대화에 대한 계약을 적용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE SERVICE service_name  
   [ AUTHORIZATION owner_name ]  
   ON QUEUE [ schema_name. ]queue_name  
   [ ( contract_name | [DEFAULT][ ,...n ] ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *service_name*  
 생성할 서비스의 이름입니다. 새 서비스는 현재 데이터베이스에 생성되며 AUTHORIZATION 절에서 지정한 주체가 소유합니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다. *service_name* 은 유효한 **sysname**합니다.  
  
> [!NOTE]  
>  만들지 마십시오 키워드를 사용 하는 서비스에 대 한 모든는 *service_name*합니다. CREATE BROKER PRIORITY에서 서비스 이름에 ANY를 지정하면 모든 서비스에 대해 우선 순위가 고려됩니다. 이러한 규칙은 이름이 ANY인 서비스로 제한되지 않습니다.  
  
 권한 부여 *owner_name*  
 서비스 소유자를 지정된 데이터베이스 사용자 또는 역할로 설정합니다. 현재 사용자가 **dbo** 또는 **sa**, *owner_name* 유효한 사용자 또는 역할의 이름일 수 있습니다. 그렇지 않으면 *owner_name* 현재 사용자의 이름, 현재 사용자가을 대 한 IMPERSONATE 권한이 있는 사용자의 이름 또는 현재 사용자가 속해 있는 역할의 이름 이어야 합니다.  
  
 ON 큐 [ *schema_name***합니다.** ] *queue_name*  
 서비스에 대한 메시지를 받는 큐를 지정합니다. 이 큐는 서비스와 같은 데이터베이스에 있어야 합니다. 없는 경우 *schema_name* 스키마는 문을 실행 하는 사용자에 대 한 기본 스키마가 제공 됩니다.  
  
 *contract_name*  
 이 서비스를 대상으로 하는 계약을 지정합니다. 서비스 프로그램은 지정된 계약을 사용하여 이 서비스에 대한 대화를 시작합니다. 계약을 지정하지 않으면 이 서비스에서만 대화를 시작할 수 있습니다.  
  
 **[**기본**]**  
 서비스가 DEFAULT 계약을 준수하는 대화의 대상이 될 수 있음을 지정합니다. 이 절의 컨텍스트에서 DEFAULT는 키워드가 아니므로 식별자로 구분해야 합니다. DEFAULT 계약을 사용하면 대화 양측이 DEFAULT 메시지 유형의 메시지를 보낼 수 있습니다. DEFAULT 메시지 유형은 유효성 검사 NONE을 사용합니다.  
  
## <a name="remarks"></a>주의  
 서비스는 연결된 계약에 의해 제공되는 기능을 노출시키므로 다른 서비스에서도 이 기능을 사용할 수 있습니다. CREATE SERVICE 문은 이 서비스를 대상으로 하는 계약을 지정합니다. 서비스는 서비스가 지정한 계약을 사용하는 대화에 대해서만 대상이 될 수 있습니다. 계약을 지정하지 않은 서비스는 기능을 다른 서비스에 노출시키지 않습니다.  
  
 이 서비스에서 시작된 대화는 모든 계약을 사용할 수 있습니다. 이 서비스만 대화를 시작할 경우 계약을 지정하지 않고 서비스를 만들 수 있습니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 원격 서비스로부터 새 대화를 허용하는 경우 Service Broker에서 대화 메시지를 넣는 큐는 대상 서비스의 이름에 의해 결정됩니다.  
  
## <a name="permissions"></a>Permissions  
 멤버에 게 서비스를 만들기 위한 권한은 기본적으로 설정 된 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할 및 **sysadmin** 고정된 서버 역할입니다. CREATE SERVICE 문을 실행하는 사용자에게는 큐 및 지정된 모든 계약에 대한 REFERENCES 권한이 있어야 합니다.  
  
 서비스에 대 한 REFERENCES 권한은 기본적으로 서비스의 구성원의 소유자는 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버는 **sysadmin** 고정된 서버 역할입니다. 서비스의 구성원의 소유자에 게 서비스 기본값에 대 한 송신 권한을 **db_owner** 고정 데이터베이스 역할의 멤버는 **sysadmin** 고정된 서버 역할입니다.  
  
 서비스는 임시 개체일 수 없습니다. 서비스 이름을  **#**  수 있지만 영구 개체입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-service-with-one-contract"></a>1. 하나의 계약이 있는 서비스 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 스키마의 `ExpenseQueue` 큐에 `dbo` 서비스를 만듭니다. 이 서비스를 대상으로 하는 대화는 `//Adventure-Works.com/Expenses/ExpenseSubmission` 계약을 준수해야 합니다.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE [dbo].[ExpenseQueue]  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="b-creating-a-service-with-multiple-contracts"></a>2. 여러 계약이 있는 서비스 만들기  
 다음 예에서는 `//Adventure-Works.com/Expenses` 큐에 `ExpenseQueue` 서비스를 만듭니다. 이 서비스를 대상으로 하는 대화는 `//Adventure-Works.com/Expenses/ExpenseSubmission` 또는 `//Adventure-Works.com/Expenses/ExpenseProcessing` 계약을 준수해야 합니다.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission],  
     [//Adventure-Works.com/Expenses/ExpenseProcessing]) ;  
```  
  
### <a name="c-creating-a-service-with-no-contracts"></a>3. 계약이 없는 서비스 만들기  
 다음 예제에서는 서비스를 만들고 `//Adventure-Works.com/Expenses on the ExpenseQueue` 큐입니다. 이 서비스에는 계약 정보가 없습니다. 그러므로 이 서비스만 대화의 시작자가 될 수 있습니다.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [서비스 &#40; 변경 Transact SQL &#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [DROP 서비스 &#40; Transact SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
