---
description: dbo.sysproxylogin(Transact-SQL)
title: dbo.sysproxylogin (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bafbc9a0e8712d0d81bed477e21f6932f3a47694
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446619"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 SQL Server 에이전트 프록시 계정에 연결되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 기록합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정의 ID입니다. 이 값은 **sysproxies** 테이블의 **proxy_id** 열에 해당 합니다.|  
|**sid**|**varbinary(85)**|SQL Server 로그인에 대 한 Microsoft Windows *security_identifier* 입니다.|  
|**principal_id**|**int**|지정된 하위 시스템 단계에 프록시 계정을 사용할 수 있는 권한이 있는 사용자 또는 그룹의 ID입니다.|  
|**flags**|**int**|로그인 유형은 다음과 같습니다.<br /><br /> **0** = Windows 사용자 또는 그룹 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정 시스템 역할<br /><br /> **2**  =  **msdb** 데이터베이스 역할|  
  
## <a name="remarks"></a>설명  
 **Sysadmin** 고정 서버 역할의 멤버만이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ Transact-sql&#41;&#40;dbo.sys프록시 ](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
