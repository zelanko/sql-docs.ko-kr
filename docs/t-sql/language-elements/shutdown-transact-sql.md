---
title: "종료 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs: TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e4cf8ea2b61d4f1acb69ea489a5116a701264469
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL Server 즉시 중지합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>인수  
 WITH NOWAIT  
 (선택 사항) 모든 데이터베이스에서 검사점을 수행하지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 종료합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모든 사용자 프로세스를 종료한 후 종료됩니다. 서버를 다시 시작하면 완료되지 않은 트랜잭션에 대해 롤백 작업이 수행됩니다.  
  
## <a name="remarks"></a>주의  
 종료 종료 WITHNOWAIT 옵션을 사용 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 여:  
  
1.  로그인을 비활성화 (의 구성원 제외는 **sysadmin** 및 **serveradmin** 고정 서버 역할)입니다.  
  
    > [!NOTE]  
    >  모든 현재 사용자의 목록을 표시 하려면 실행 **sp_who**합니다.  
  
2.  현재 실행하는 Transact-SQL 문이나 저장 프로시저가 완료되기를 기다립니다. 모든 활성 프로세스 및 잠금의 목록을 표시 하려면 실행 **sp_who** 및 **sp_lock**각각.  
  
3.  모든 데이터베이스에 검사점을 삽입합니다.  
  
 SHUTDOWN 문을 사용 하 여 최소화 되는 작업 필요한 경우 자동 복구의의 멤버는 **sysadmin** 고정 서버 역할 다시 시작 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 다른 도구 및 방법을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지할 수도 있습니다. 각 방법은 모든 데이터베이스에서 검사점을 실행합니다. 데이터 캐시에서 커밋된 데이터를 플러시하고 서버를 중지할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용합니다.  
  
-   실행 하 여 **net stop mssqlserver** 기본 인스턴스를 실행 하거나 명령 프롬프트에서 **net stop mssql$ * * * instancename* 명명 된 인스턴스의 명령 프롬프트에서 합니다.  
  
-   제어판에서 서비스를 사용합니다.  
  
 경우 **sqlservr.exe** 시작한 명령 프롬프트에서 CTRL + C를 누르면 종료 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 그러나 Ctrl+C를 눌러도 검사점이 삽입되지는 않습니다.  
  
> [!NOTE]  
>  이 방법 중 하나를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지하면 `SERVICE_CONTROL_STOP` 메시지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 전송됩니다.  
  
## <a name="permissions"></a>Permissions  
 SHUTDOWN 권한은의 멤버에 할당 되는 **sysadmin** 및 **serveradmin** 고정된 서버 역할을 받지 않습니다 양도할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Checkpoint&#40; Transact SQL &#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr 응용 프로그램](../../tools/sqlservr-application.md)   
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
