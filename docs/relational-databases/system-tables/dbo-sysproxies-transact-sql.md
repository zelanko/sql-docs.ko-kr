---
title: dbo.sysproxies (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a37300ad1bf16ac76fbcbd0c6e77870077f7f631
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470602"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정의 특성을 정의합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|프록시 계정의 ID입니다.|  
|**name**|**sysname**|프록시 계정의 이름입니다.|  
|**credential_id**|**int**|프록시 계정이 사용하는 자격 증명의 ID입니다.|  
|**enabled**|**tinyint**|프록시 계정의 상태입니다.<br /><br /> **0** = 사용 안 함. **1** = 사용 하도록 설정 합니다.|  
|**description**|**nvarchar(512)**|프록시 계정을 만들 때 사용자가 입력한 설명입니다.|  
|**user_sid**|**varbinary(85)**|Microsoft Windows *security_identifier* 사용자 또는 프록시 자격 증명을 사용 하 여 연결 된 그룹입니다.|  
|**credential_date_created**|**datetime**|자격 증명을 작성한 날짜와 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 구성원만 합니다 **sysadmin** 고정된 서버 역할에 액세스할 수 합니다 **sysproxies** 테이블입니다.  
  
## <a name="see-also"></a>관련 항목  
 [dbo.sysproxylogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
