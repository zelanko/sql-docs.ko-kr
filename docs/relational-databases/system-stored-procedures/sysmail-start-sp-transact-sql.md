---
title: sysmail_start_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9789d454961e9bb22e5d35c36b4be47056ef7739
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailstartsp-transact-sql"></a>sysmail_start_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  외부 프로그램이 사용하는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 개체를 시작하여 데이터베이스 메일을 시작합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>인수  
 InclusionThresholdSetting  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 데이터베이스 메일 하지 않을 지 설치 된[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다. 데이터베이스 메일 구성 마법사를 사용하여 데이터베이스 메일 개체를 설정하고 설치할 수 있습니다.  
  
 이 저장된 프로시저에는 **msdb** 데이터베이스입니다. 이 저장 프로시저는 보내는 메시지 요청이 있는 데이터베이스 메일 큐를 시작하고 외부 프로그램에 대한 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 활성화를 설정합니다.  
  
 큐가 시작되면 데이터베이스 메일 외부 프로그램이 메시지를 처리할 수 있습니다. 이 절차를 사용 하면 큐 중지 된 큐를 다시 시작할 수 있습니다는 **sysmail_stop_sp** 저장 프로시저입니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 데이터베이스 메일에 대한 큐만 시작합니다. 이 저장 프로시저는 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달을 활성화하지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 메일 시작 하는 **msdb** 데이터베이스입니다. 이 예에서는 데이터베이스 메일이 설정되었다고 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail XPs 서버 구성 옵션](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [sysmail_stop_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [데이터베이스 메일 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
