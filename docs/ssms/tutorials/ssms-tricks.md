---
Title: 'Tutorial: Additional Tips and Tricks for using SSMS'
description: 'SSMS 사용에 대한 추가 팁과 요령을 다루는 자습서입니다. '
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
ms.openlocfilehash: 792d6c7fe69a1b8ec77c70d0fbfa6ceaa92d808a
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>자습서: SSMS 사용을 위한 추가 팁과 요령
이 자습서에서는 SQL Server Management Studio를 사용하기 위한 몇 가지 추가 요령을 제공합니다. 이 문서는 다음 방법을 설명합니다. 

> [!div class="checklist"]
> * T-SQL(Transact-SQL) 텍스트 주석 처리/주석 처리 제거
> * 텍스트 들여쓰기
> * 개체 탐색기에서 개체 필터링
> * SQL Server 오류 로그에 액세스
> * SQL Server 인스턴스의 이름 찾기

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio, SQL Server에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하기 위한 지침은 여기: [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)에서 찾을 수 있습니다. 

## <a name="comment--uncomment-your-t-sql-code"></a>T-SQL 코드 주석 처리/주석 처리 제거
도구 모음의 주석 단추를 사용하여 텍스트의 부분을 주석 처리 및 주석 처리 제거할 수 있습니다. 주석 처리한 텍스트를 실행할 수 없습니다. 

1. SQL Server Management Studio를 엽니다. 
2. SQL Server에 연결합니다.
3. **새 쿼리** 창을 엽니다. 
4. 다음 T-SQL 코드 조각을 텍스트 창에 붙여넣습니다. 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 


5. 텍스트의 **데이터베이스 변경** 부분을 강조 표시하고 도구 모음에서 **주석**을 클릭합니다. 

    ![설명](media/ssms-tricks/comment.png)
6. **실행**을 클릭하여 텍스트의 주석 처리가 제거된 부분을 실행합니다. 
7. **데이터베이스 변경** 명령 이외의 모든 항목을 강조 표시하고 도구 모음에서 **주석**을 클릭합니다.

    ![모든 항목 주석 처리](media/ssms-tricks/commenteverything.png)

8. **데이터베이스 변경** 부분을 강조 표시하고 **주석 처리 제거**를 클릭하여 주석 처리를 제거합니다.

    ![주석 처리 제거](media/ssms-tricks/uncomment.png)
    
9. **실행**을 클릭하여 텍스트의 주석 처리가 제거된 부분을 실행합니다. 

## <a name="indent-your-text"></a>텍스트 들여쓰기
들여쓰기 단추를 사용하여 텍스트의 들여쓰기를 늘리거나 줄일 수 있습니다. 

1. **새 쿼리** 창을 엽니다. 
2. 다음 T-SQL 코드 조각을 텍스트 창에 붙여넣습니다. 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 
 
3. 텍스트의 **데이터베이스 변경** 부분을 강조 표시하고 도구 모음의 **들여쓰기**를 눌러 이 텍스트를 앞으로 이동합니다.

    ![들여쓰기](media/ssms-tricks/increaseindent.png)

4. 텍스트의 **데이터베이스 변경** 부분을 다시 강조 표시하고 이번에는 **내어쓰기**를 클릭하여 이 텍스트를 뒤로 이동합니다. 
    ![내어쓰기](media/ssms-tricks/decreaseindent.png)


## <a name="filter-objects-in-object-explorer"></a>개체 탐색기에서 개체 필터링
데이터베이스에 많은 개체가 있는 경우 특정 개체를 찾기 어려울 수 있습니다. 간단하게 하기 위해 개체를 필터링하는 기능이 있습니다. 이 섹션에서는 테이블을 필터링하는 방법을 설명하지만 **개체 탐색기** 내의 다른 노드에 동일한 단계를 적용할 수 있습니다.

1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. **AdventureWorks** 데이터베이스 노드를 확장합니다. 
4. **테이블** 노드를 확장합니다. 
   - 데이터베이스에 있는 모든 테이블을 볼 수 있는 것을 확인할 수 있습니다.
5. 마우스 오른쪽 단추로 **테이블** 노드 > **필터** > **필터 설정**을 클릭합니다.

    ![필터 설정](media/ssms-tricks/filtersettings.png)

6. 필터 설정 창에서 필터 설정을 수정할 수 있습니다. 몇 가지 예제:
    - 이름으로 필터링: ![이름으로 필터링](media/ssms-tricks/filterbyname.png)
    - 스키마로 필터링: ![스키마로 필터링](media/ssms-tricks/filterbyschema.png)

7. 필터를 지우려면 마우스 오른쪽 단추로 **테이블** > **필터 제거**를 클릭합니다.

    ![필터 제거](media/ssms-tricks/removefilter.png)
    


## <a name="access-your-sql-server-error-log"></a>SQL Server 오류 로그에 액세스
오류 로그는 SQL Server 내에서 발생하는 작업에 대한 세부 정보를 포함하는 파일입니다. SSMS 내에서 찾고 쿼리할 수 있습니다. 디스크에서 .log 파일로 찾을 수도 있습니다.

### <a name="open-error-log-within-ssms"></a>SSMS 내에서 오류 로그 열기
1. SQL Server에 연결합니다.
2. **관리** 노드를 확장합니다. 
3. **SQL Server 로그** 노드를 확장합니다. 
4. **현재** 오류 로그 > **SQL Server 로그 보기**를 마우스 오른쪽 단추로 클릭합니다.

    ![SSMS 내에서 오류 로그 보기](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-error-log-within-ssms"></a>SSMS 내에서 오류 로그 쿼리
1. SQL Server에 연결합니다.
2. **새 쿼리** 창을 엽니다.
3. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣습니다.

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 
4. 작은따옴표의 텍스트를 원하는 텍스트로 수정합니다.
5. 쿼리를 실행하고 결과를 검토합니다.
   
    ![오류 로그 쿼리](media/ssms-tricks/queryerrorlog.png)


### <a name="find-error-log-location-if-youre-connected-to-sql"></a>SQL에 연결된 경우 오류 로그 위치 찾기
1. SQL Server에 연결
2. **새 쿼리** 창을 엽니다.
3. 다음 T-SQL 코드 조각을 쿼리 창에 붙여넣고 **실행**을 클릭합니다.

 ```sql
    SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
  ``` 

4. 결과는 파일 시스템 내에서 오류 로그의 위치를 보여줍니다. 

    ![쿼리로 오류 로그 찾기](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-error-log-location-if-you-cannot-connect-to-sql"></a>SQL에 연결할 수 없는 경우 오류 로그 위치 찾기
1. SQL Server 구성 관리자를 엽니다. 
2. **서비스** 노드를 확장합니다.
3. SQL Server 인스턴스 > **속성**을 마우스 오른쪽 단추로 클릭합니다.

    ![구성 관리자 서버 속성](media/ssms-tricks/serverproperties.PNG)

4. **시작 매개 변수** 탭을 선택합니다.
5. **기존 매개 변수** 영역에서 "-e" 뒤의 경로는 오류 로그의 위치입니다. 
    
    ![오류 로그](media/ssms-tricks/errorlog.png)
    - 이 위치에 여러 errorlog.*가 있는 것을 확인할 수 있습니다. *.log로 끝나는 것이 현재 오류 로그입니다. 숫자로 끝나는 것은 SQL Server가 다시 시작될 때마다 새 로그가 생성되므로 이전 로그입니다. 
6. 메모장에서 이 파일을 엽니다. 

## <a name="determine-sql-server-name"></a>SQL Server 이름 확인...
SQL Server에 연결하기 전후에 SQL Server의 이름을 확인하는 여러 가지 방법이 있습니다.  

### <a name="when-you-dont-know-it"></a>...알지 못하는 경우
1. 단계를 따라 [디스크의 SQL Server 오류 로그](#finding-your-error-log-if-you-cannot-connect-to-sql)를 찾습니다. 
2. 메모장에서 errorlog.log를 엽니다. 
3. "서버 이름은" 텍스트를 찾을 때까지 탐색합니다.
  - 작은따옴표에 나열된 것은 SQL Server의 이름 및 연결할 항목(![오류 로그의 서버 이름](media/ssms-tricks/servernameinlog.png))입니다. 이름의 서식은 'HOSTNAME\INSTANCENAME'입니다. 표시되는 항목이 호스트 이름인 경우 기본 인스턴스를 설치했고 인스턴스 이름은 'MSSQLSERVER'입니다. 기본 인스턴스에 연결할 때 호스트 이름만 입력하면 SQL Server에 연결됩니다.  

### <a name="once-youre-connected-to-sql"></a>...SQL에 연결된 후 
연결된 SQL Server를 찾는 세 가지 위치가 있습니다. 

1. 서버의 이름은 **개체 탐색기**에 나열됩니다.

    ![개체 탐색기에서 인스턴스 이름](media/ssms-tricks/nameinobjectexplorer.png)
2. 서버의 이름은 쿼리 창에 나열됩니다.

    ![쿼리 창에서 이름](media/ssms-tricks/nameinquerywindow.png)
3. 서버의 이름은 **속성 창**에도 나열됩니다.
    - 여기에 액세스하려면 **보기** 메뉴 > **속성 창**을 엽니다.

    ![속성의 이름](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>...별칭 또는 가용성 그룹 수신기에 연결된 경우 
별칭 또는 가용성 그룹 수신기에 연결된 경우 **개체 탐색기** 및 **속성**을 표시합니다. 이 경우 SQL Server 이름을 즉시 확인할 수 없으며 쿼리해야 합니다. 

1. SQL Server에 연결합니다.
2. **새 쿼리** 창을 엽니다.
3. 다음 T-SQL 코드 조각을 창에 붙여넣습니다. 

  ```sql
   select @@Servername 
 ``` 
4. 연결된 SQL Server의 이름을 식별하려면 쿼리의 결과를 봅니다. 
    
    ![쿼리 서버 이름](media/ssms-tricks/queryservername.png)


