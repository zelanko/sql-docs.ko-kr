---
description: sp_changedistributor_property(Transact-SQL)
title: sp_changedistributor_property (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributor_property_TSQL
- sp_changedistributor_property
helpviewer_keywords:
- sp_changedistributor_property
ms.assetid: 04f503a1-307c-4de0-bac6-e6e97d5b6940
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 284f669f81f0954c0a9676d5f7a4ab8a213eba58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464439"
---
# <a name="sp_changedistributor_property-transact-sql"></a>sp_changedistributor_property(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  배포자의 속성을 변경합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changedistributor_property [ [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @property = ] 'property'` 지정 된 배포자의 속성입니다. *속성* 은 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**heartbeat_interval**|진행률 메시지를 기록하지 않고 에이전트를 실행할 수 있는 최대 시간(분)입니다.|  
|NULL(기본값)|사용 가능한 모든 *속성* 값이 출력 됩니다.|  
  
`[ @value = ] 'value'` 지정 된 배포자 속성에 대 한 값입니다. *값* 은 **varchar (255)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changedistributor_property** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pro_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_changedistributor_property**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Transact-sql&#41;sp_adddistributor &#40;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [Transact-sql&#41;sp_dropdistributor &#40;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
