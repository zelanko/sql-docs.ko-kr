---
title: sp_helpserver (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: aa1a9a5841f5b43a6dea6f0650a7686f499b4965
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258595"
---
# <a name="sphelpserver-transact-sql"></a>sp_helpserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 원격 또는 복제 서버나 두 유형의 서버 모두에 관한 정보를 보고합니다. 서버 이름, 서버의 네트워크 이름, 서버의 복제 상태, 서버의 ID, 데이터 정렬 이름을 제공합니다. 연결된 서버 연결 또는 쿼리 제한 시간 값도 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@server =** ] **'***server***'**  
 정보를 보고할 대상이 되는 서버입니다. 때 *서버* 를 지정 하지 않으면 모든 서버에 대 한 보고서 **master.sys.servers**합니다. *서버* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@optname =** ] **'***옵션***'**  
 서버를 설명하는 옵션입니다. *옵션* 은 **varchar (** 35 **)**, 기본값은 NULL 이며 다음이 값 중 하나 여야 합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**데이터 정렬 호환**|연결된 서버에 대한 분산 쿼리 실행에 영향을 미칩니다. 이 옵션이 true로 설정되어 있는 경우|  
|**데이터 액세스**|분산 쿼리 액세스에 대해 연결된 서버의 사용 여부를 설정합니다.|  
|**dist**|배포자입니다.|  
|**dpub**|해당 배포자에 대한 원격 게시자입니다.|  
|**지연 된 스키마 유효성 검사**|쿼리를 시작할 때 원격 테이블의 스키마 확인을 건너뜁니다.|  
|**pub**|게시자입니다.|  
|**rpc**|지정된 서버에서 RPC를 사용하도록 설정합니다.|  
|**rpc 내보내기**|지정된 서버에 RPC를 사용하도록 설정합니다.|  
|**sub**|구독자입니다.|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**원격 데이터 정렬 사용**|로컬 서버가 아닌 원격 열의 데이터 정렬을 사용합니다.|  
  
 [  **@show_topology =** ] **'***show_topology***'**  
 지정한 서버와 다른 서버의 관계입니다. *show_topology* 은 **varchar (** 1 **)**, 기본값은 NULL입니다. 경우 *show_topology* 과 같지 않은 **t** 아니거나 null 일 경우 **sp_helpserver** 결과 집합 섹션에 나열 된 열을 반환 합니다. 경우 *show_topology* 같으면 **t**, 결과 집합에 나열 된 열과 함께 **sp_helpserver** 도 반환 **topx** 및 **topy** 정보입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패).  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|서버 이름입니다.|  
|**network_name**|**sysname**|서버의 네트워크 이름입니다.|  
|**상태**|**varchar (** 70 **)**|서버 상태입니다.|  
|**id**|**char (** 4 **)**|서버의 ID입니다.|  
|**collation_name**|**sysname**|서버의 데이터 정렬입니다.|  
|**connect_timeout**|**int**|연결된 서버에 대한 연결 시간 제한 값입니다.|  
|**query_timeout**|**int**|연결된 서버에 대한 쿼리 시간 제한 값입니다.|  
  
## <a name="remarks"></a>주의  
 서버 상태가 두 개 이상일 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 사용 권한을 확인하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-information-about-all-servers"></a>1. 모든 서버에 관한 정보 표시  
 다음 예에서는 매개 변수 없이 `sp_helpserver`를 사용하여 모든 서버에 관한 정보를 표시합니다.  
  
```  
USE master;  
GO  
EXEC sp_helpserver;  
```  
  
### <a name="b-displaying-information-about-a-specific-server"></a>2. 특정 서버에 관한 정보 표시  
 다음 예에서는 `SEATTLE2` 서버에 관한 모든 정보를 표시합니다.  
  
```  
USE master;  
GO  
EXEC sp_helpserver 'SEATTLE2';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_addsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sp_serveroption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
