---
title: sp_helpreplfailovermode (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords: sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 212775844dde7400ca3ddb17753091aa56b582f1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독의 현재 장애 조치(Failover) 모드를 표시합니다. 이 저장 프로시저는 모든 데이터베이스의 구독자에서 실행됩니다. 장애 조치 모드에 대 한 자세한 내용은 참조 [업데이트할 수 있는 Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher=**] **'***게시자***'**  
 이 구독자의 업데이트에 참여하고 있는 게시자 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다. 게시하려면 게시자가 미리 구성되어 있어야 합니다.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publication=**] **'***게시***'**  
 이 구독자의 업데이트에 참여하고 있는 게시 이름입니다. *게시*은 **sysname**, 기본값은 없습니다.  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***' 출력**  
 장애 조치 모드의 정수 값을 반환 하 고이 **출력** 매개 변수입니다. *failover_mode_id* 는 **tinyint** 기본값인 **0**합니다. 반환 **0** 즉시 업데이트 및 **1** 지연 업데이트 합니다.  
  
 [**@failover_mode=**] **'***failover_mode***' 출력**  
 구독자에서 데이터가 수정되는 모드를 반환합니다. *failover_mode* 는 **nvarchar (10)** 기본값은 NULL입니다. 이 **출력** 매개 변수입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 실행**|즉시 업데이트: 구독자에서 수행되는 업데이트가 2단계 커밋 프로토콜(2PC)을 사용하여 즉시 게시자로 전파됩니다.|  
|**큐에 대기**|지연 업데이트: 구독자에서 수행되는 업데이트가 큐에 저장됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpreplfailovermode** 업데이트 오류가 발생 한 경우 장애 조치로 지연 구독 즉시 업데이트를 사용 하도록 설정 된 트랜잭션 복제 또는 스냅숏 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_helpreplfailovermode**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_setreplfailovermode &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
