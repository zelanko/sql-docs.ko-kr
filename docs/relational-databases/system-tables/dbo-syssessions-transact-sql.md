---
title: dbo.sys세션 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 12/30/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs:
- TSQL
helpviewer_keywords:
- syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 13d57b4c36d238cb8e6893ff912e7052ba2e079f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890379"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions(Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 시작할 때마다 새 세션을 만듭니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 세션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 다시 시작되거나 갑자기 중지될 경우 작업 상태를 보존할 수 있습니다. **Syssessions** 테이블의 각 행에는 한 세션에 대 한 정보가 포함 되어 있습니다. **Sysjobactivity** 테이블을 사용 하 여 각 세션이 끝날 때 작업 상태를 볼 수 있습니다.  
  
 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 세션의 ID입니다. 이 session_id는 세션에 대 한 SPID가 아니라이 시스템 테이블의 ID 값입니다.|  
|**agent_start_date**|**datetime**|이 세션에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작된 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>설명  
 **Sysadmin** 고정 서버 역할의 멤버인 사용자만이 테이블에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [dbo.sysjobactivity &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
