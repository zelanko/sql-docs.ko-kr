---
title: "데이터베이스 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [SQL Server], creating
- database creation [SQL Server], SQL Server Management Studio
- creating databases
ms.assetid: 4c4beea2-6cbc-4352-9db6-49ea8130bb64
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6b0ae1c495b1e8405a43eb0900c03c2eec55ca35
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-database"></a>데이터베이스 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 데이터베이스를 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스당 최대 32,767개의 데이터베이스를 지정할 수 있습니다.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   CREATE DATABASE 문은 기본 트랜잭션 관리 모드인 자동 커밋 모드에서 실행해야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   사용자 데이터베이스를 생성, 수정 또는 삭제할 때마다 [master](../../relational-databases/databases/master-database.md) 데이터베이스를 백업해야 합니다.  
  
-   데이터베이스를 만들 때는 데이터베이스에서 예상되는 최대 데이터 크기를 고려하여 데이터 파일을 가능한 한 크게 만드는 것이 좋습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 master 데이터베이스의 CREATE DATABASE 권한이 있거나 CREATE ANY DATABASE 또는 ALTER ANY DATABASE 권한이 있어야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디스크 사용을 제어하기 위해 일반적으로 데이터베이스를 만들 수 있는 사용 권한은 일부 로그인 계정으로 제한됩니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-database"></a>데이터베이스를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 클릭합니다.  
  
3.  **새 데이터베이스**에 데이터베이스 이름을 입력합니다.  
  
4.  모든 기본값을 사용하여 데이터베이스를 만들려면 **확인**을 클릭합니다. 그렇지 않으면 다음 옵션 단계로 계속 진행합니다.  
  
5.  소유자 이름을 변경하려면 (**…**)을 클릭하여 다른 소유자를 선택합니다.  
  
    > [!NOTE]  
    >  **부터 모든 사용자 데이터베이스에서 전체 텍스트를 사용할 수 있기 때문에** 전체 텍스트 인덱싱 사용 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]옵션이 항상 선택되어 있고 흐리게 표시됩니다.  
  
6.  주 데이터 및 트랜잭션 로그 파일의 기본값을 변경하려면 **데이터베이스 파일** 표에서 해당 셀을 클릭하고 새 값을 입력합니다. 자세한 내용은 [Add Data or Log Files to a Database](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)을 참조하세요.  
  
7.  데이터베이스의 데이터 정렬을 변경하려면 **옵션** 페이지를 선택한 다음 목록에서 데이터 정렬을 선택합니다.  
  
8.  복구 모델을 변경하려면 **옵션** 페이지를 선택하고 목록에서 복구 모델을 선택합니다.  
  
9. 데이터베이스 옵션을 변경하려면 **옵션** 페이지를 선택한 다음 데이터베이스 옵션을 수정합니다. 각 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
10. 새 파일 그룹을 추가하려면 **파일 그룹** 페이지를 클릭합니다. **추가** 를 클릭한 다음 파일 그룹의 값을 입력합니다.  
  
11. 데이터베이스에 확장 속성을 추가하려면 **확장 속성** 페이지를 선택합니다.  
  
    1.  **이름** 열에 확장 속성의 이름을 입력합니다.  
  
    2.  **값** 열에 확장 속성 텍스트를 입력합니다. 예를 들어 데이터베이스에 대해 설명하는 하나 이상의 문을 입력할 수 있습니다.  
  
12. 데이터베이스를 만들려면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-database"></a>데이터베이스를 만들려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 `Sales`데이터베이스를 만듭니다. 주 키워드를 사용하지 않았으므로 첫 번째 파일(`Sales_dat`)이 주 파일이 됩니다. `Sales_dat` 파일의 SIZE 매개 변수에 MB 또는 KB를 지정하지 않았으므로 기본값 MB를 사용하여 할당됩니다. 사용자 데이터베이스를 생성, 수정 또는 삭제할 때마다 `Sales_log` 파일은 `MB` 매개 변수에 명시적으로 `SIZE` 접미사를 지정했으므로 메가바이트(MB)로 공간이 할당됩니다.  
  
```tsql  
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
 추가 예제를 보려면 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스에 데이터 또는 로그 파일 추가](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
  
  
