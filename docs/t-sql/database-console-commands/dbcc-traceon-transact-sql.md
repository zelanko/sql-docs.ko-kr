---
title: DBCC TRACEON(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_TRACEON_TSQL
- TRACEON
- DBCC TRACEON
- TRACEON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC TRACEON statement
- trace flags [SQL Server], enabling
ms.assetid: 93085324-ebaa-4e38-aac8-5e57b4b0d36d
author: pmasl
ms.author: umajay
ms.openlocfilehash: c1bf9d7182e7547a69e7b5cd634c07ff2130c9cc
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485561"
---
# <a name="dbcc-traceon-transact-sql"></a>DBCC TRACEON(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

지정한 추적 플래그를 설정합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DBCC TRACEON ( trace# [ ,...n ][ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*trace#*  
설정할 추적 플래그의 개수입니다.  
  
*n*  
여러 개의 추적 플래그를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
-1  
지정한 추적 플래그를 전역으로 설정합니다. 이 인수는 Azure SQL Managed Instance에 필요합니다. 
  
WITH NO_INFOMSGS  
모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>설명  
예기치 않은 상황이 발생하지 않도록 다음 방법 중 하나를 사용하여 프로덕션 서버에서 서버 차원의 추적 플래그만 설정하는 것이 좋습니다.
-   Sqlservr.exe의 **-T** 명령줄 시작 옵션을 사용합니다. 모든 문이 추적 플래그가 설정된 상태에서 실행되므로 이 방법이 최선의 구현 방법입니다. 여기에는 시작 스크립트의 명령이 포함됩니다. 자세한 내용은 [sqlservr Application](../../tools/sqlservr-application.md)을 참조하세요.  
-   사용자 또는 애플리케이션이 시스템에서 동시에 명령문을 실행하지 않는 동안에만 DBCC TRACEON **(** _trace#_ [ **,** ... *.n*] **,-1)** 을 사용합니다.  

추적 플래그는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 작동하는 방법을 제어하여 특정한 특징을 사용자 지정하는 데 사용됩니다. 설정된 추적 플래그는 DBCC TRACEOFF 문을 실행하여 해제할 때까지 서버에서 설정된 상태로 유지됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 세션 및 전역이라는 두 가지 유형의 추적 플래그가 있습니다. 세션 추적 플래그는 특정 연결에 대해 설정되며 해당 연결에서만 볼 수 있습니다. 전역 추적 플래그는 서버 수준에서 설정되며 서버의 모든 연결에서 볼 수 있습니다. 추적 플래그의 상태를 확인하려면 DBCC TRACESTATUS를 사용하십시오. 추적 플래그를 해제하려면 DBCC TRACEOFF를 사용하십시오.
  
쿼리 계획에 영향을 주는 추적 플래그를 켠 후, 새 계획에 영향을 주는 동작을 사용하여 캐시된 계획이 다시 컴파일되도록 `DBCC FREEPROCCACHE;`를 실행합니다.

Azure SQL Database Managed Instance는 전역 추적 플래그 460,2301,2389,2390,2453,2467,7471,8207,9389,10316 및 11024를 지원합니다.

## <a name="result-sets"></a>결과 집합  
 DBCC TRACEON은 다음 결과 집합(메시지)을 반환합니다.  
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>사용 권한  
**sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.
  
## <a name="examples"></a>예  
다음 예에서는 `3205` 추적 플래그를 설정하여 테이프 드라이버에 대한 하드웨어 압축을 해제합니다. 이 플래그는 현재 연결에 대해서만 설정됩니다.
  
```sql  
DBCC TRACEON (3205);  
GO  
```  
  
다음 예에서는 `3205` 추적 플래그를 전역으로 설정합니다.
  
```sql  
DBCC TRACEON (3205, -1);  
GO  
```  
  
다음 예에서는 `3205` 및 `260` 추적 플래그를 전역으로 설정합니다.
  
```sql  
DBCC TRACEON (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACESTATUS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
[특정 쿼리 수준에서 여러 다른 추적 플래그를 통해 제어할 수 있는 계획에 영향을 주는 SQL Server 쿼리 최적화 프로그램 동작 설정](https://support.microsoft.com/kb/2801413)
  
  
