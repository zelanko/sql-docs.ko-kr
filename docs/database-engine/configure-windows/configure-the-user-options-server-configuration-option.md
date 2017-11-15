---
title: "user options 서버 구성 옵션 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- global default for all users [SQL Server]
- users [SQL Server], global defaults
- user options option [SQL Server]
ms.assetid: cfed8f86-6bcf-4b90-88eb-9656e22d5dc5
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f50c084a5f546a27f3152ed55ea4796225193ed4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-user-options-server-configuration-option"></a>user options 서버 구성 옵션 구성
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] user options [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **user options** 옵션은 모든 사용자에 대한 전역 기본값을 지정합니다. 기본 쿼리 처리 옵션 목록은 사용자의 작업 세션 기간에 대해 설정됩니다. **user options** 옵션을 사용하면 서버의 기본 설정이 적합하지 않은 경우 SET 옵션의 기본값을 변경할 수 있습니다.  
  
 사용자는 SET 문을 사용하여 이 기본값을 무시할 수 있습니다. 새로운 로그인에 대해 **user options** 를 동적으로 구성할 수 있습니다. **user options**설정을 변경하고 나면 새 로그인이 새 설정을 사용합니다. 현재 로그인에는 영향을 주지 않습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 user options 구성 옵션을 구성합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [user options 구성 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   다음 표에서는 **user options**에 따른 구성 값을 나열하고 설명합니다. 모든 구성 값은 서로 호환 됩니다. 예를 들어 ANSI_NULL_DFLT_ON 및 ANSI_NULL_DFLT_OFF는 동시에 설정할 수 없습니다.  
  
    |값|Configuration|설명|  
    |-----------|-------------------|-----------------|  
    |1|DISABLE_DEF_CNST_CHK|중간 또는 지연된 제약 조건 검사를 제어합니다.|  
    |2|IMPLICIT_TRANSACTIONS|dblib 네트워크 라이브러리 연결의 경우 문 실행 시 트랜잭션을 암시적으로 시작할지 여부를 제어합니다. IMPLICIT_TRANSACTIONS 설정은 ODBC 또는 OLEDB 연결에 영향을 주지 않습니다.|  
    |4|CURSOR_CLOSE_ON_COMMIT|커밋 작업 수행 후 커서의 동작을 제어합니다.|  
    |8|ANSI_WARNINGS|집계 경고의 잘림과 NULL을 제어합니다.|  
    |16|ANSI_PADDING|고정 길이 변수의 패딩을 제어합니다.|  
    |32|ANSI_NULLS|동등 연산자 사용 시 NULL 처리를 제어합니다.|  
    |64|ARITHABORT|쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다.|  
    |128|ARITHIGNORE|쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 NULL을 반환합니다.|  
    |256|QUOTED_IDENTIFIER|식을 평가할 때 큰따옴표와 작은따옴표를 구분합니다.|  
    |512|NOCOUNT|영향 받는 행 수를 지정하는 각 문의 끝에 반환되는 메시지를 해제합니다.|  
    |1024|ANSI_NULL_DFLT_ON|세션에서 Null 허용에 대해 ANSI 호환성을 사용할 때 경고합니다. 명시적 Null 허용 없이 정의된 새 열은 Null을 허용하도록 정의됩니다.|  
    |2048|ANSI_NULL_DFLT_OFF|세션이 null 허용에 대해 ANSI 호환성을 사용하지 않을 때 경고합니다. 명시적인 NULL 허용 없이 정의된 새 열은 NULL을 허용하지 않습니다.|  
    |4096|CONCAT_NULL_YIELDS_NULL|문자열이 있는 NULL 값을 연결할 때 NULL을 반환합니다.|  
    |8192|NUMERIC_ROUNDABORT|식의 전체 자릿수가 떨어지면 오류가 발생합니다.|  
    |16384|XACT_ABORT|Transact-SQL 문이 런타임 오류를 일으키면 트랜잭션을 롤백합니다.|  
  
-   **user options**의 비트 위치는 @@OPTIONS의 비트 위치와 같습니다. 각 연결에는 구성 환경을 나타내는 @@OPTIONS 함수가 있습니다. \ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그인하면 현재 **user options** 값을 @@OPTIONS에 할당하는 기본 환경이 사용자에게 표시됩니다. **user options**에 대한 SET 문을 실행하면 세션의 @@OPTIONS 함수에 해당하는 값에 영향을 줍니다. 이 설정이 변경된 이후에 만들어진 모든 연결은 새 값을 받습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>user options 구성 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **연결** 노드를 클릭합니다.  
  
3.  **기본 연결 옵션** 상자에서 하나 이상의 특성을 선택하여 연결된 모든 사용자의 기본 쿼리 처리 옵션을 구성합니다.  
  
     기본적으로 사용자 옵션은 구성되어 있지 않습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>user options 구성 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 통해 ANSI_WARNINGS 서버 옵션에 대한 설정을 변경하기 위해 `user options` 으로 설정하여 제한 시간을 사용하지 않도록 설정하는 방법을 보여 줍니다.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'user options', 8 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
##  <a name="FollowUp"></a> 후속 작업: user options 구성 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
