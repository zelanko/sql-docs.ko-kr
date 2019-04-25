---
title: dbo.sysproxylogin (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxylogin_TSQL
- sysproxylogin_TSQL
- dbo.sysproxylogin
- sysproxylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxylogin system table
ms.assetid: 433d33cb-bdf2-47bb-af78-2a40b7c8dfce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00a3b3b53bcede7f43aad556465358b957331f45
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470695"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 SQL Server 에이전트 프록시 계정에 연결되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 기록합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정의 ID입니다. 이 값에 해당 합니다 **proxy_id** 열에는 **sysproxies** 테이블입니다.|  
|**sid**|**varbinary(85)**|Microsoft Windows *security_identifier* SQL Server 로그인에 대 한 합니다.|  
|**principal_id**|**int**|지정된 하위 시스템 단계에 프록시 계정을 사용할 수 있는 권한이 있는 사용자 또는 그룹의 ID입니다.|  
|**flags**|**int**|로그인 유형은 다음과 같습니다.<br /><br /> **0** = Windows 사용자 또는 그룹 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 합니다.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정된 시스템 역할<br /><br /> **2** = **msdb** 데이터베이스 역할|  
  
## <a name="remarks"></a>Remarks  
 멤버는 **sysadmin** 고정된 서버 역할이이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [dbo.sysproxies &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
