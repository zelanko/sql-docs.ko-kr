---
title: SSMS 사용 팁과 요령
description: 코드를 주석 처리하거나 주석 처리를 제거하고, 텍스트를 들여쓰고, 개체 탐색기에서 개체를 필터링하고, SQL Server 오류 로그에 액세스하고, SQL Server Management Studio를 사용하여 SQL Server 인스턴스 이름을 찾는 방법을 알아봅니다.
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
author: MashaMSFT
ms.author: mathoma
ms.reviewer: sstein
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- Find SQL Server Instance
- find instance name
- find sql server instance name
ms.custom: seo-lt-2019
ms.date: 03/13/2018
ms.openlocfilehash: 7a07e4cd77d02e4c62c34e55eedbd3dbf01c8322
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75245506"
---
# <a name="tips-and-tricks-for-using-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하기 위한 팁과 요령

이 문서에서는 SSMS(SQL Server Management Studio)를 사용하기 위한 몇 가지 팁과 요령을 제공합니다. 이 아티클에서는 다음을 수행하는 방법을 보여줍니다. 

> [!div class="checklist"]
> * T-SQL(Transact-SQL) 텍스트 주석 처리/주석 처리 제거
> * 텍스트 들여쓰기
> * 개체 탐색기에서 개체 필터링
> * SQL Server 오류 로그에 액세스
> * SQL Server 인스턴스의 이름 찾기

## <a name="prerequisites"></a>사전 요구 사항

이 문서에 제공된 단계를 테스트하려면 SQL Server Management Studio, SQL Server 액세스 및 AdventureWorks 데이터베이스가 필요합니다. 

* [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
* [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
* [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하는 방법을 자세히 알아보려면 [데이터베이스 복원](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요. 

## <a name="commentuncomment-your-t-sql-code"></a>T-SQL 코드 주석 처리/주석 처리 제거

도구 모음의 **주석** 단추를 사용하여 텍스트의 일부를 주석 처리하고 주석 처리를 제거할 수 있습니다. 주석 처리한 텍스트를 실행할 수 없습니다.

1. SQL Server Management Studio를 엽니다.

2. SQL Server에 연결합니다.

3. 새 쿼리 창을 엽니다.

4. 다음 T-SQL 코드를 텍스트 창에 붙여넣습니다.

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

5. 텍스트의 **데이터베이스 변경** 부분을 강조 표시한 다음, 도구 모음에서 **주석**을 선택합니다. 

    ![주석 단추](media/ssms-tricks/comment.png)
6. **실행**을 선택하여 텍스트의 주석 처리가 제거된 부분을 실행합니다. 

7. **데이터베이스 변경** 명령을 제외한 모든 항목을 강조 표시한 다음, **주석** 단추를 선택합니다.

    ![모든 항목 주석 처리](media/ssms-tricks/commenteverything.png)

    > [!NOTE]
    > 텍스트 주석 처리에 대한 바로 가기 키는 **CTRL+K, CTRL+C**입니다.

8. 텍스트의 **데이터베이스 변경** 부분을 강조 표시한 다음, **주석 처리 제거** 단추를 선택하여 주석 처리를 제거합니다.

    ![텍스트 주석 처리 제거](media/ssms-tricks/uncomment.png)

    > [!NOTE]
    > 텍스트 주석 처리 해제에 대한 바로 가기 키는 **CTRL+K, CTRL+U**입니다.

9. **실행**을 선택하여 텍스트의 주석 처리가 제거된 부분을 실행합니다.

## <a name="indent-your-text"></a>텍스트 들여쓰기

도구 모음의 들여쓰기 단추를 사용하여 텍스트의 들여쓰거나 내어쓸 수 있습니다.

1. 새 쿼리 창을 엽니다.

2. 다음 T-SQL 코드를 텍스트 창에 붙여넣습니다.

    ```sql
    USE master
      GO

      --Drop the database if it already exists
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

3. 텍스트의 **데이터베이스 변경** 부분을 강조 표시한 다음, 도구 모음의 **들여쓰기** 단추를 선택하여 이 텍스트를 앞으로 이동합니다.

    ![들여쓰기](media/ssms-tricks/increaseindent.png)

4. 텍스트의 **데이터베이스 변경** 부분을 다시 강조 표시한 다음, **내어쓰기** 단추를 선택하여 이 텍스트를 뒤로 이동합니다.

    ![내어쓰기](media/ssms-tricks/decreaseindent.png)

## <a name="filter-objects-in-object-explorer"></a>개체 탐색기에서 개체 필터링

많은 개체가 있는 데이터베이스에서 필터링을 사용하여 특정 테이블, 뷰 등을 검색할 수 있습니다. 이 섹션에서는 테이블을 필터링하는 방법을 설명하지만 개체 탐색기의 다른 노드에서 다음 단계를 사용할 수 있습니다.

1. SQL Server에 연결합니다.

2. **데이터베이스** > **AdventureWorks** > **테이블**을 확장합니다. 데이터베이스의 모든 테이블이 표시됩니다.

3. **테이블**을 마우스 오른쪽 단추로 클릭한 다음, **필터** > **필터 설정**을 선택합니다.

    ![필터 설정](media/ssms-tricks/filtersettings.png)

4. **필터 설정** 창에서 다음과 같은 일부 필터 설정을 수정할 수 있습니다.
    * 이름으로 필터링: 

      ![이름으로 필터링](media/ssms-tricks/filterbyname.png)

    * 스키마로 필터링: 

      ![스키마로 필터링](media/ssms-tricks/filterbyschema.png)

5. 필터를 지우려면 **테이블**을 마우스 오른쪽 단추로 클릭한 다음, **필터 제거**를 선택합니다.

    ![필터 제거](media/ssms-tricks/removefilter.png)

## <a name="access-your-sql-server-error-log"></a>SQL Server 오류 로그에 액세스

오류 로그는 SQL Server 인스턴스에서 발생하는 작업에 대한 세부 정보를 포함하는 파일입니다. SSMS에서 오류 로그를 찾아보고 쿼리할 수 있습니다. 오류 로그는 디스크에 있는.log 파일입니다.

### <a name="open-the-error-log-in-ssms"></a>SSMS에서 오류 로그 열기

1. SQL Server에 연결합니다.  

2. **관리** > **SQL Server 로그**를 확장합니다. 

3. **현재** 오류 로그를 마우스 오른쪽 단추로 클릭한 다음, **SQL Server 로그 보기**를 선택합니다.

    ![SSMS에서 오류 로그 보기](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-the-error-log-in-ssms"></a>SSMS에서 오류 로그 쿼리

1. SQL Server에 연결합니다.

2. 새 쿼리 창을 엽니다.

3. 다음 T-SQL 코드를 쿼리 창에 붙여넣습니다.

     ```sql
       sp_readerrorlog 0,1,'Server process ID'
      ```

4. 작은따옴표의 텍스트를 검색하려는 텍스트로 수정합니다.

5. 쿼리를 실행한 다음, 결과를 검토합니다.

    ![오류 로그 쿼리](media/ssms-tricks/queryerrorlog.png)

### <a name="find-the-error-log-location-if-youre-connected-to-sql-server"></a>SQL Server에 연결된 경우 오류 로그 위치 찾기

1. SQL Server에 연결합니다.

2. 새 쿼리 창을 엽니다.

3. 다음 T-SQL 코드를 쿼리 창에 붙여넣은 다음, **실행**을 선택합니다.

     ```sql
        SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
      ```

4. 결과는 파일 시스템에서 오류 로그의 위치를 보여줍니다. 

    ![쿼리로 오류 로그 찾기](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-the-error-log-location-if-you-cant-connect-to-sql-server"></a>SQL Server에 연결할 수 없는 경우 오류 로그 위치 찾기

SQL Server 오류 로그에 대한 경로는 구성 설정에 따라 다를 수 있습니다. 오류 로그 위치에 대한 경로는 SQL Server 구성 관리자 내의 시작 매개 변수에서 찾을 수 있습니다. 아래 단계에 따라 SQL Server 오류 로그의 위치를 식별하는 관련 시작 매개 변수를 찾습니다. *경로는 아래 표시된 경로와 다를 수 있습니다*.

1. SQL Server 구성 관리자를 엽니다.

2. **서비스**를 확장합니다.

3. SQL Server 인스턴스를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.

    ![Configuration Manager 서버 속성](media/ssms-tricks/serverproperties.PNG)

4. **시작 매개 변수** 탭을 선택합니다.

5. **기존 매개 변수** 영역에서 "-e" 뒤의 경로는 오류 로그의 위치입니다. 

    ![오류 로그](media/ssms-tricks/errorlog.png)

    이 위치에 여러 개의 errorlog.* 파일이 있습니다. *.log로 끝나는 파일 이름은 현재 오류 로그 파일입니다. 숫자로 끝나는 파일 이름은 이전 로그 파일입니다. SQL Server를 다시 시작할 때마다 새 로그가 생성됩니다.

6. 메모장에서 errorlog.log 파일을 엽니다. 

## <a name="determine-sql-server-name"></a>SQL Server 인스턴스 이름 찾기

SQL Server에 연결한 전후에 SQL Server의 이름을 찾는 몇 가지 옵션이 있습니다.  

### <a name="before-you-connect-to-sql-server"></a>SQL Server에 연결하기 전에

1. 단계를 따라 [디스크의 SQL Server 오류 로그](#find-the-error-log-location-if-you-cant-connect-to-sql-server)를 찾습니다. 경로는 아래 이미지의 경로와 다를 수 있습니다.

2. 메모장에서 errorlog.log 파일을 엽니다.

3. *서버 이름은* 텍스트를 검색합니다.

    작은따옴표에 나열된 것은 연결하려는 SQL Server 인스턴스의 이름입니다.

    ![오류 로그에서 서버 이름 찾기](media/ssms-tricks/servernameinlog.png)

    이름의 형식은 HOSTNAME\INSTANCENAME입니다. 호스트 이름만 표시되는 경우 기본 인스턴스를 설치했고 인스턴스 이름은 MSSQLSERVER입니다. 기본 인스턴스에 연결할 때 호스트 이름만 입력하면 SQL Server에 연결됩니다.  

### <a name="when-youre-connected-to-sql-server"></a>SQL Server에 연결된 경우

SQL Server에 연결된 경우 세 개의 위치에서 서버 이름을 찾을 수 있습니다. 

1. 서버의 이름은 개체 탐색기에 나열됩니다.

    ![개체 탐색기의 SQL Server 인스턴스 이름](media/ssms-tricks/nameinobjectexplorer.png)
2. 서버의 이름은 쿼리 창에 나열됩니다.

    ![쿼리 창의 SQL Server 인스턴스 이름](media/ssms-tricks/nameinquerywindow.png)
3. 서버의 이름은 **속성**에 나열됩니다.
    * **보기** 메뉴에서 **속성 창**을 선택합니다.

      ![속성 창의 SQL Server 인스턴스 이름](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>별칭 또는 가용성 그룹 수신기에 연결된 경우

별칭 또는 가용성 그룹 수신기에 연결된 경우 해당 정보가 개체 탐색기 및 속성에 표시됩니다. 이 경우에 SQL Server 이름을 즉시 확인할 수 없으며 쿼리해야 합니다.

1. SQL Server에 연결합니다.

2. 새 쿼리 창을 엽니다.

3. 다음 T-SQL 코드를 창에 붙여넣습니다.

      ```sql
       select @@Servername
     ```

4. 연결된 SQL Server 인스턴스의 이름을 식별하려면 쿼리의 결과를 봅니다. 

    ![SQL Server 이름 쿼리](media/ssms-tricks/queryservername.png)

## <a name="next-steps"></a>다음 단계

실습을 통해 SSMS에 익숙해지는 것이 가장 좋습니다. 이러한 *자습서* 및 *방법* 문서에서는 SSMS 내에서 사용할 수 있는 다양한 기능에 관해 도움을 얻을 수 있습니다.  이러한 문서에서는 SSMS의 구성 요소를 관리하는 방법과 정기적으로 사용하는 기능을 찾는 방법을 알아봅니다.

* [인스턴스에 연결 및 쿼리](connect-query-sql-server.md)
* [스크립팅](scripting-ssms.md)
* [SSMS에서 템플릿 사용](../template/templates-ssms.md)
* [SSMS 구성](ssms-configuration.md)
