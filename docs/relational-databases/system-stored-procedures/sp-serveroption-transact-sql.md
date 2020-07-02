---
title: sp_serveroption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_serveroption_TSQL
- sp_serveroption
dev_langs:
- TSQL
helpviewer_keywords:
- 7343 (Database Engine error)
- sp_serveroption
ms.assetid: 47d04a2b-dbf0-4f15-bd9b-81a2efc48131
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 933774af820c80abb70c5fbdad0441053533b451
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783713"
---
# <a name="sp_serveroption-transact-sql"></a>sp_serveroption(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  원격 서버 및 연결된 서버용 서버 옵션을 설정합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>인수  
`[ @server = ] 'server'`옵션을 설정할 서버의 이름입니다. *server* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @optname = ] 'option_name'`지정 된 서버에 대해 설정할 수 있는 옵션입니다. *option_name* 는 **varchar (** 35 **)** 이며 기본값은 없습니다. *option_name* 은 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**데이터 정렬 호환**|연결된 서버에 대한 분산 쿼리 실행에 영향을 줍니다. 이 옵션을 **true**로 설정 하면에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 된 서버의 모든 문자가 문자 집합 및 데이터 정렬 시퀀스 (또는 정렬 순서)와 관련 하 여 로컬 서버와 호환 된다고 가정 합니다. 이렇게 함으로써 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 문자 열에 관한 비교를 공급자에 전달할 수 있습니다. 이 옵션을 설정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 항상 문자 열에 관한 비교를 로컬로 평가합니다.<br /><br /> 이 옵션은 연결된 서버에 해당되는 데이터 원본이 로컬 서버와 동일한 문자 집합 및 정렬 순서를 갖고 있는 것이 확실한 경우에만 설정해야 합니다.|  
|**데이터 정렬 이름**|원격 데이터 **정렬 사용** 이 **true** 이 고 데이터 원본이 데이터 원본이 아닌 경우 원격 데이터 원본에서 사용 하는 데이터 정렬의 이름을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이름은 반드시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 데이터 정렬 중 하나여야 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 OLE DB 데이터 원본에 액세스할 때 해당 데이터 정렬이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 중 하나와 일치하면 이 옵션을 사용하세요.<br /><br /> 연결된 서버는 반드시 해당 서버의 모든 열에 대해 사용할 단일 데이터 정렬을 지원해야 합니다. 연결된 서버에서 단일 데이터 원본 내에 여러 데이터 정렬을 지원하거나 연결된 서버의 데이터 정렬이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 중 하나와 일치하는지 확인할 수 없는 경우에는 이 옵션을 사용하지 않습니다.|  
|**연결 시간 제한**|연결 된 서버에 연결 하기 위한 제한 시간 (초)입니다.<br /><br /> **0**인 경우 **sp_configure** 기본값을 사용 합니다.|  
|**데이터 액세스**|분산 쿼리 액세스에 대해 연결된 서버의 사용 여부를 설정합니다. 는 **sp_addlinkedserver**를 통해 추가 된 **서버** 항목에만 사용할 수 있습니다.|  
|**dist**|배포자입니다.|  
|**지연된 스키마 유효성 검사**|원격 테이블의 스키마 확인 여부를 결정합니다.<br /><br /> **True**이면 쿼리 시작 부분에 있는 원격 테이블의 스키마 검사를 건너뜁니다.|  
|**pub**|게시자입니다.|  
|**쿼리 제한 시간**|연결된 서버에 대한 쿼리의 제한 시간 값입니다.<br /><br /> **0**인 경우 **sp_configure** 기본값을 사용 합니다.|  
|**상관**|지정된 서버로부터의 RPC가 가능하도록 합니다.|  
|**rpc 아웃**|지정된 서버로의 RPC가 가능하도록 합니다.|  
|**sub**|구독자입니다.|  
|**시스템**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**원격 데이터 정렬 사용**|원격 열의 데이터 정렬을 사용할지 로컬 서버의 데이터 정렬을 사용할지 결정합니다.<br /><br /> **True**이면 데이터 원본에 원격 열의 데이터 정렬이 사용 되 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 데이터 정렬 **이름** 에 지정 된 데이터 정렬은 비 데이터 원본에 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> **False**이면 분산 쿼리에서 항상 로컬 서버의 기본 데이터 정렬을 사용 하 고, **데이터 정렬 이름** 및 원격 열의 데이터 정렬은 무시 됩니다. 기본값은 **false**입니다. **False** 값은 7.0에서 사용 되는 데이터 정렬 의미 체계와 호환 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**remote proc transaction promotion**|이 옵션을 사용하여 MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) 트랜잭션을 통해 서버 간 프로시저 동작을 보호할 수 있습니다. 이 옵션이 TRUE(또는 ON)인 경우 원격 저장 프로시저를 호출하면 분산 트랜잭션이 시작되고 MS DTC를 사용해 이 트랜잭션을 참여시킵니다. 원격 저장 프로시저를 호출하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 트랜잭션 주관자이며 트랜잭션의 완료를 제어합니다. 이후 연결에 대해 COMMIT TRANSACTION 또는 ROLLBACK TRANSACTION 문을 실행하면 제어 인스턴스는 MS DTC에서 관련 컴퓨터 간의 분산 트랜잭션 완료를 관리하도록 요청합니다.<br /><br /> [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션이 시작되면 연결된 서버로 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스에 대해 원격 저장 프로시저를 호출할 수 있습니다. 연결된 서버를 모두 [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션에 참여시키고 MS DTC는 각 연결된 서버에 대해 트랜잭션이 완료되도록 합니다.<br /><br /> 이 옵션을 FALSE(또는 OFF)로 설정하면 연결된 서버에서 원격 프로시저를 호출하는 동안에는 로컬 트랜잭션이 분산 트랜잭션으로 승격되지 않습니다.<br /><br /> 서버 간 프로시저 호출을 수행하기 전에 트랜잭션이 이미 분산 트랜잭션인 경우 이 옵션은 영향을 주지 않습니다. 연결된 서버에 대한 프로시저 호출은 동일 분산 트랜잭션에서 실행됩니다.<br /><br /> 서버 간 프로시저 호출을 수행하기 전에 연결에 활성 상태인 트랜잭션이 없는 경우 이 옵션은 영향을 주지 않습니다. 그런 다음 활성 상태의 트랜잭션 없이 연결된 서버에 대해 프로시저가 실행됩니다.<br /><br /> 이 옵션의 기본값은 TRUE(또는 ON)입니다.|  
  
`[ @optvalue = ] 'option_value'`*Option_name* 사용 하도록 설정 (**TRUE** 또는 **on**) 하거나 사용 하지 않도록 (**FALSE** 또는 **off**) 여부를 지정 합니다. *option_value* 는 **varchar (** 10 **)** 이며 기본값은 없습니다.  
  
 **연결 시간 제한** 및 **쿼리 제한 시간** 옵션에 대 한 *option_value* 는 음수가 아닌 정수일 수 있습니다. **Collation name** 옵션의 경우 데이터 정렬 이름이 나 NULL 일 수 *option_value* .  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **데이터 정렬 호환** 옵션이 TRUE로 설정 된 경우 **데이터 정렬 이름이** 자동으로 NULL로 설정 됩니다. **데이터 정렬 이름이** null이 아닌 값으로 설정 된 경우 **데이터 정렬 호환** 이 자동으로 FALSE로 설정 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LINKED SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스인 `SEATTLE3`에 해당하는 연결된 서버를 구성하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스와 데이터 정렬이 호환되도록 합니다.  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;분산 쿼리 저장 프로시저](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_adddistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_addlinkedserver &#40;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Transact-sql&#41;sp_dropdistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_helpserver &#40;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
