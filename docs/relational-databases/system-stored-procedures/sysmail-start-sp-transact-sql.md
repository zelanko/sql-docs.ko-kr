---
description: sysmail_start_sp(Transact-SQL)
title: sysmail_start_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c0a4bda3849a5863ce5ed87e25cafdc7983f49f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469110"
---
# <a name="sysmail_start_sp-transact-sql"></a>sysmail_start_sp(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  외부 프로그램이 사용하는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 개체를 시작하여 데이터베이스 메일을 시작합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>인수  
 None  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 설정되거나 설치되지 않습니다. 데이터베이스 메일 구성 마법사를 사용하여 데이터베이스 메일 개체를 설정하고 설치할 수 있습니다.  
  
 이 저장 프로시저는 **msdb** 데이터베이스에 있습니다. 이 저장 프로시저는 보내는 메시지 요청이 있는 데이터베이스 메일 큐를 시작하고 외부 프로그램에 대한 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 활성화를 설정합니다.  
  
 큐가 시작되면 데이터베이스 메일 외부 프로그램이 메시지를 처리할 수 있습니다. 이 절차를 사용 하면 **sysmail_stop_sp** 저장 프로시저를 사용 하 여 큐가 중지 된 후 큐를 다시 시작할 수 있습니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 데이터베이스 메일에 대한 큐만 시작합니다. 이 저장 프로시저는 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달을 활성화하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 **msdb** 데이터베이스에서 데이터베이스 메일를 시작 하는 방법을 보여 줍니다. 이 예에서는 데이터베이스 메일이 설정되었다고 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 XPs 서버 구성 옵션](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [Transact-sql&#41;sysmail_stop_sp &#40;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
