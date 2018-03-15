---
title: GO(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- GO
- GO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- batches [SQL Server], ending
- ending batches [SQL Server]
- GO command
ms.assetid: b2ca6791-3a07-4209-ba8e-2248a92dd738
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 63fe775455df2b9b25ec3abc8bb0208aa6b5dd0e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="sql-server-utilities-statements---go"></a>SQL Server 유틸리티 문 - GO
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **sqlcmd** 및 **osql** 유틸리티와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 코드 편집기에서 인식되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 아닌 명령을 제공합니다. 이러한 명령을 사용하면 일괄 처리 및 스크립트를 쉽게 읽고 실행할 수 있습니다.  
  
  GO는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 일괄 처리의 끝을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 알립니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GO [count]  
```  
  
## <a name="arguments"></a>인수  
 *count*  
 양의 정수입니다. GO 앞의 일괄 처리가 지정된 횟수만큼 실행됩니다.  
  
## <a name="remarks"></a>Remarks  
 GO는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 아니라 **sqlcmd** 및 **osql** 유틸리티와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 코드 편집기에서 인식되는 명령입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 현재 일괄 처리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 보내야 함을 나타내는 신호로 GO를 해석합니다. 문의 현재 일괄 처리는 첫 번째 GO의 경우 임시 세션이나 스크립트가 시작된 이후 또는 마지막 GO 이후에 입력된 모든 문으로 구성됩니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 GO 명령과 동일한 줄에 지정할 수 없습니다. 그러나 해당 줄에 주석이 포함될 수는 있습니다.  
  
 사용자는 일괄 처리 규칙을 따라야 합니다. 예를 들어 일괄 처리에서 첫 번째 문 다음에 실행되는 저장 프로시저에는 EXECUTE 키워드가 들어 있어야 합니다. 사용자 정의 지역 변수의 범위는 일괄 처리로 제한되므로 GO 명령 다음에 참조될 수 없습니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyMsg VARCHAR(50)  
SELECT @MyMsg = 'Hello, World.'  
GO -- @MyMsg is not valid after this GO ends the batch.  
  
-- Yields an error because @MyMsg not declared in this batch.  
PRINT @MyMsg  
GO  
  
SELECT @@VERSION;  
-- Yields an error: Must be EXEC sp_who if not first statement in   
-- batch.  
sp_who  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램에서는 여러 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 일괄 처리로 실행하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 보낼 수 있습니다. 그러면 일괄 처리에 있는 문은 단일 실행 계획으로 컴파일됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 임시 문을 실행하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 유틸리티를 통해 실행되도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문의 스크립트를 작성하는 프로그래머는 GO를 사용하여 일괄 처리의 끝을 알립니다.  
  
 ODBC 또는 OLE DB API를 기반으로 하는 응용 프로그램에서 GO 명령을 실행하려고 하면 구문 오류가 발생합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 GO 명령을 서버로 보내지 않습니다.  
  
 GO 후에는 문 종결자로 세미콜론을 사용하지 마십시오.  
  
## <a name="permissions"></a>사용 권한  
 GO는 사용 권한이 필요 없는 유틸리티 명령입니다. 모든 사용자가 실행할 수 있습니다.  
  
```  
-- Yields an error because ; is not permitted after GO  
SELECT @@VERSION;  
GO;  
```  
  
## <a name="examples"></a>예  
 다음 예에서는 일괄 처리를 두 개 만듭니다. 첫 번째 일괄 처리에는 데이터베이스 컨텍스트를 설정하는 `USE``AdventureWorks2012` 문만 있습니다. 나머지 문에는 지역 변수를 사용합니다. 따라서 모든 지역 변수 선언을 단일 일괄 처리로 그룹화해야 합니다. 변수를 참조하는 마지막 문 다음까지 `GO` 명령을 사용하지 않으면 됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NmbrPeople int  
SELECT @NmbrPeople = COUNT(*)  
FROM Person.Person;  
PRINT 'The number of people as of ' +  
      CAST(GETDATE() AS char(20)) + ' is ' +  
      CAST(@NmbrPeople AS char (10));  
GO  
```  
  
 다음 예에서는 일괄 처리에서 문을 두 번 실행합니다.  
  
```  
SELECT DB_NAME();  
SELECT USER_NAME();  
GO 2  
```  
  
  
