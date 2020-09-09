---
description: dbo.sysproxies(Transact-SQL)
title: dbo.sys프록시 (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d806ed58647b8c22edd28be44e85790b1962e32a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540425"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정의 특성을 정의합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|프록시 계정의 ID입니다.|  
|**name**|**sysname**|프록시 계정의 이름입니다.|  
|**credential_id**|**int**|프록시 계정이 사용하는 자격 증명의 ID입니다.|  
|**사용**|**tinyint**|프록시 계정의 상태입니다.<br /><br /> **0** = 사용 안 함 **1** = 사용|  
|**description**|**nvarchar(512)**|프록시 계정을 만들 때 사용자가 입력한 설명입니다.|  
|**user_sid**|**varbinary(85)**|프록시 자격 증명과 연결 된 사용자 또는 그룹의 Microsoft Windows *security_identifier* 입니다.|  
|**credential_date_created**|**datetime**|자격 증명을 작성한 날짜와 시간입니다.|  
  
## <a name="remarks"></a>설명  
 **Sysadmin** 고정 서버 역할의 멤버만 **sysproxies** 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [dbo.sysproxylogin &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sys하위 시스템 &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
