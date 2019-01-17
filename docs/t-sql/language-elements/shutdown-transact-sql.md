---
title: SHUTDOWN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 602c8f5d1cded1c5d19c520087ceac1b9c9124d5
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591897"
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL Server를 즉시 중지합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>인수  
 WITH NOWAIT  
 (선택 사항) 모든 데이터베이스에서 검사점을 수행하지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 종료합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모든 사용자 프로세스를 종료한 후 종료됩니다. 서버를 다시 시작하면 완료되지 않은 트랜잭션에 대해 롤백 작업이 수행됩니다.  
  
## <a name="remarks"></a>Remarks  
 WITHNOWAIT 옵션을 사용하지 않으면 SHUTDOWN은 다음을 수행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 종료합니다.  
  
1.  **sysadmin** 및 **serveradmin** 고정 서버 역할의 멤버를 제외하고 로그인을 비활성화합니다.  
  
    > [!NOTE]  
    >  현재의 모든 사용자에 대한 목록을 표시하려면 **sp_who**를 실행합니다.  
  
2.  현재 실행하는 Transact-SQL 문이나 저장 프로시저가 완료되기를 기다립니다. 모든 활성 프로세스 및 잠금의 목록을 표시하려면 **sp_who** 및 **sp_lock**을 각각 실행합니다.  
  
3.  모든 데이터베이스에 검사점을 삽입합니다.  
  
 SHUTDOWN 문을 사용하면 **sysadmin** 고정 서버 역할의 멤버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 때 필요한 자동 복구 작업량이 최소화됩니다.  
  
 다른 도구 및 방법을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지할 수도 있습니다. 각 방법은 모든 데이터베이스에서 검사점을 실행합니다. 데이터 캐시에서 커밋된 데이터를 플러시하고 서버를 중지할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용합니다.  
  
-   기본 인스턴스의 명령 프롬프트에서 **net stop mssqlserver**를 실행하거나 명명된 인스턴스에 대한 명령 프롬프트에서 **net stop mssql$**_instancename_을 실행합니다.  
  
-   제어판에서 서비스를 사용합니다.  
  
 명령 프롬프트에서 **sqlservr.exe**를 시작한 경우 Ctrl+C를 누르면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 종료됩니다. 그러나 Ctrl+C를 눌러도 검사점이 삽입되지는 않습니다.  
  
> [!NOTE]  
>  이 방법 중 하나를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지하면 `SERVICE_CONTROL_STOP` 메시지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 전송됩니다.  
  
## <a name="permissions"></a>Permissions  
 SHUTDOWN 권한은 **sysadmin** 및 **serveradmin** 고정 서버 역할의 멤버에게 할당되며, 양도할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CHECKPOINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr 애플리케이션](../../tools/sqlservr-application.md)   
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
