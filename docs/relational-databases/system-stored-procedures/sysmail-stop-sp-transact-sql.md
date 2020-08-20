---
description: sysmail_stop_sp(Transact-SQL)
title: sysmail_stop_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6630ddcb05645422ba2049636637a3e480e543c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473352"
---
# <a name="sysmail_stop_sp-transact-sql"></a>sysmail_stop_sp(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  외부 프로그램이 사용하는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 개체를 중지하여 데이터베이스 메일을 중지합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>인수  
 None  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 **msdb** 데이터베이스에 있습니다.  
  
 이 저장 프로시저는 보내는 메시지 요청이 있는 데이터베이스 메일 큐를 중지하고 외부 프로그램에 대한 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 활성화를 해제합니다.  
  
 큐가 중지되면 데이터베이스 메일 외부 프로그램이 메시지를 처리할 수 없습니다. 이 저장 프로시저를 통해 문제 해결 또는 유지 관리 목적으로 데이터베이스 메일을 중지할 수 있습니다.  
  
 데이터베이스 메일를 시작 하려면 **sysmail_start_sp**를 사용 합니다. 개체가 중지 될 때에도 **sp_send_dbmail** 메일을 수락 하는 것을 볼 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 수 있습니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 데이터베이스 메일의 큐만 중지합니다. 이 저장 프로시저는 데이터베이스에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달을 비활성화하지 않습니다. 이 저장 프로시저는 데이터베이스 메일 확장 저장 프로시저를 해제하여 노출 영역을 줄일 수 없습니다. 확장 저장 프로시저를 사용 하지 않도록 설정 하려면 **sp_configure** 시스템 저장 프로시저의 [데이터베이스 메일 XPs 옵션](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) 을 참조 하십시오.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 **msdb** 데이터베이스에서 데이터베이스 메일를 중지 하는 방법을 보여 줍니다. 이 예에서는 데이터베이스 메일이 설정되었다고 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [Transact-sql&#41;sysmail_start_sp &#40;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
