---
title: 테이블 또는 인덱스에 압축 사용 | Microsoft 문서
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 SQL Server에서 테이블 또는 인덱스에 대한 압축을 사용하도록 설정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.compwiz.compressiontype.f1
- sql13.swb.compwiz.outputoptions.f1
- sql13.swb.compwiz.summary.f1
- sql13.swb.compwiz.scriptfileoption.f1
- sql13.swb.compwiz.progress.f1
- sql13.swb.compwiz.welcome.f1
- sql13.swb.compwiz.createjob.f1
- sql13.swb.compwiz.selectaction.f1
helpviewer_keywords:
- data compression wizard
- compression [SQL Server], enable
ms.assetid: b7442cff-e616-475a-9c5a-5a765089e5f2
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016'
ms.openlocfilehash: 080d50b76d71d7a0c13104f20303fe040d214a33
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485505"
---
# <a name="enable-compression-on-a-table-or-index"></a>테이블 또는 인덱스에 압축 사용

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 테이블이나 인덱스에 압축을 사용하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 테이블이나 인덱스에 압축 사용**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   시스템 테이블에는 압축을 사용할 수 없습니다.  
  
-   테이블이 힙인 경우 ONLINE 모드의 다시 작성 작업은 단일 스레드 작업이 됩니다. 다중 스레드 힙 다시 작성 작업에는 OFFLINE 모드를 사용하세요. 데이터 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
-   테이블에 정렬되지 않은 인덱스가 있으면 단일 파티션의 압축 설정을 변경할 수 없습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블이나 인덱스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-enable-compression-on-a-table-or-index"></a>테이블이나 인덱스에 압축을 사용하려면  
  
1.  개체 탐색기에서 압축할 테이블이 포함된 데이터베이스를 확장한 다음 **테이블** 폴더를 확장합니다.  
  
2.  인덱스를 압축하려면 압축할 인덱스가 포함된 테이블을 확장한 다음 **인덱스** 폴더를 확장합니다.  
  
3.  압축할 테이블이나 인덱스를 마우스 오른쪽 단추로 클릭하고 **스토리지** 를 가리킨 다음, **압축 관리...** 를 선택합니다.  
  
4.  데이터 압축 마법사의 **데이터 압축 마법사 시작** 페이지에서 **다음** 을 클릭합니다.  
  
5.  **압축 유형 선택** 페이지에서 압축할 테이블이나 인덱스의 각 파티션에 적용할 압축 유형을 선택합니다. 완료되면 **다음** 을 클릭합니다.  
  
     다음은 **압축 유형 선택** 페이지에서 선택할 수 있는 옵션입니다.  
  
     **모든 파티션에 동일한 압축 유형 사용** 확인란  
     모든 파티션에 동일한 압축 설정을 구성하려면 선택합니다. 이렇게 하면 선택 상자가 활성화되고 표의 **압축 유형** 열이 비활성화됩니다 이 옵션을 선택하면 인접 목록의 옵션은 **없음**, **행** 및 **페이지** 입니다.  
  
     **파티션 번호**  
     테이블이나 인덱스에 있는 각 파티션을 나열합니다. 이 열은 읽기 전용입니다.  
  
     **압축 유형**  
     각 파티션의 압축 옵션을 선택합니다. **모든 파티션에 동일한 압축 유형 사용** 을 선택한 경우에는 사용할 수 없습니다. 목록의 옵션은 **없음**, **행** 및 **페이지** 입니다.  
  
     **경계**  
     파티션 경계를 표시합니다. 이 열은 읽기 전용입니다.  
  
     **행 개수**  
     이 파티션의 행 수를 표시합니다. 이 열은 읽기 전용입니다.  
  
     **현재 공간**  
     이 파티션이 차지하는 현재 공간(MB)을 표시합니다. 이 열은 읽기 전용입니다.  
  
     **요청한 압축 공간**  
     **계산** 을 클릭하면 **압축 유형** 열에서 지정한 설정을 사용하여 압축 후 각 파티션의 예상 크기가 이 열에 표시됩니다. 이 열은 읽기 전용입니다.  
  
     **계산**  
     **압축 유형** 열에서 지정한 설정을 사용하여 압축 후 각 파티션의 크기를 예측하려면 클릭합니다.  
  
6.  **출력 옵션 선택** 페이지에서 압축을 완료하는 방법을 지정합니다. 마법사의 이전 페이지를 기반으로 SQL 스크립트를 만들려면 **스크립트 만들기** 를 선택합니다. 마법사의 남은 페이지를 모두 완료한 후 새 분할된 테이블을 만들려면 **즉시 실행** 을 선택합니다. 향후 미리 결정된 시간에 새 분할된 테이블을 만들려면 **일정** 을 선택합니다.  
  
     **스크립트 만들기** 를 선택하는 경우 **스크립트 옵션** 에서 다음과 같은 옵션을 사용할 수 있습니다.  
  
     **파일로 스크립팅**  
     스크립트를 .sql 파일로 생성합니다. **파일 이름** 상자에 파일 이름 및 위치를 입력하거나 **찾아보기** 를 클릭하여 **스크립트 파일 위치** 대화 상자를 엽니다. **다른 이름으로 저장** 에서 **유니코드 텍스트** 또는 **ANSI 텍스트** 를 선택합니다.  
  
     **클립보드로 스크립팅**  
     스크립트를 클립보드에 저장합니다.  
  
     **새 쿼리 창으로 스크립팅**  
     새 쿼리 편집기 창에 스크립트를 생성합니다. 이 옵션이 기본 옵션입니다.  
  
     **일정** 을 선택하는 경우 **일정 변경** 을 클릭합니다.  
  
    1.  **새 작업 일정** 대화 상자의 **이름** 상자에 작업 일정 이름을 입력합니다.  
  
    2.  **일정 유형** 목록에서 다음과 같은 일정 유형을 선택합니다.  
  
        -   **SQL Server 에이전트가 시작될 때 자동으로 시작**  
  
        -   **CPU가 유휴 상태로 될 때마다 시작**  
  
        -   **되풀이**. 새 분할된 테이블을 정기적으로 새로운 정보로 업데이트하는 경우 이 옵션을 선택합니다.  
  
        -   **한 번**. 이 옵션이 기본 옵션입니다.  
  
    3.  일정을 사용하거나 사용하지 않으려면 **사용** 확인란을 선택하거나 선택을 취소합니다.  
  
    4.  **되풀이** 를 선택하는 경우 다음을 수행합니다.  
  
        1.  **빈도** 아래의 **되풀이** 목록에서 다음과 같이 발생 빈도를 지정합니다.  
  
            -   **일별** 을 선택하는 경우 **매** 상자에 작업 일정을 반복하는 일 수를 입력합니다.  
  
            -   **주별** 을 선택하는 경우 **매** 상자에 작업 일정을 반복하는 주 수를 입력합니다. 작업 일정을 실행할 요일을 선택합니다.  
  
            -   **월별** 을 선택한 경우 **매(Day)** 또는 **매(The)** 를 선택합니다.  
  
                -   **매(Day)** 를 선택한 경우 작업 일정을 실행할 날짜와 작업 일정을 반복할 월 수를 모두 입력합니다. 예를 들어 작업 일정을 격월로 15일에 실행하려면 **매(Day)** 를 선택하고 첫 번째 상자에 "15", 두 번째 상자에 "2"를 입력합니다. 두 번째 상자에 허용되는 가장 큰 숫자는 "99"입니다.  
  
                -   **매(The)** 를 선택한 경우 작업 일정을 실행할 요일 및 작업 일정을 반복할 월 수를 입력합니다. 예를 들어 작업 일정을 격월로 마지막 평일에 실행하려면 **매(Day)** 를 선택하고 첫 번째 목록에서 **마지막**, 두 번째 목록에서 **평일** 을 선택한 다음, 마지막 상자에 "2"를 입력합니다. **첫 번째**, **두 번째**, **세 번째** 또는 **네 번째** 또는 특정 평일(예: 일요일 또는 수요일)을 선택할 수도 있습니다. 마지막 상자에 허용되는 가장 큰 숫자는 "99"입니다.  
  
        2.  **일별 빈도** 에서 작업 일정이 실행되는 날에 작업 일정을 반복하는 빈도를 지정합니다.  
  
            -   **한 번 수행** 을 선택하는 경우 **한 번 수행** 상자에 작업 일정을 실행할 특정 시간을 입력합니다. 시간, 분, 초와 오전 또는 오후를 입력합니다.  
  
            -   **되풀이 수행** 을 선택하는 경우 **빈도** 에 선택한 날 동안 작업 일정을 실행할 빈도를 지정합니다. 예를 들어 작업 일정을 실행하는 날에 2시간마다 작업 일정을 반복하려면 **되풀이 수행** 을 선택하고 첫 번째 상자에 "2"를 입력한 다음, 목록에서 **시간** 을 선택합니다. 이 목록에서 **분** 과 **초** 도 선택할 수 있습니다. 첫 번째 상자에 허용되는 가장 큰 숫자는 "100"입니다.  
  
                 **시작** 상자에 작업 일정 실행을 시작할 시간을 입력합니다. **종료** 상자에 작업 일정 반복을 중지할 시간을 입력합니다. 시간, 분, 초와 오전 또는 오후를 입력합니다.  
  
        3.  **기간** 아래의 **시작 날짜** 에 작업 일정 실행을 시작할 날짜를 입력합니다. **종료 날짜** 또는 **종료 날짜 없음** 을 선택하여 작업 일정 실행을 중지할 시기를 나타냅니다. **종료 날짜** 를 선택하는 경우 작업 일정 실행을 중지할 날짜를 입력합니다.  
  
    5.  **한 번** 을 선택하는 경우 **한 번 발생** 아래 **날짜** 상자에 작업 일정을 실행할 날짜를 입력합니다. **시간** 상자에 작업 일정을 실행할 시간을 입력합니다. 시간, 분, 초와 오전 또는 오후를 입력합니다.  
  
    6.  **요약** 아래 **설명** 에서 모든 작업 일정 설정이 올바른지 확인합니다.  
  
    7.  **확인** 을 클릭합니다.  
  
     이 페이지를 마쳤으면 **다음** 을 클릭합니다.  
  
7.  **요약 검토** 페이지의 **선택 항목 검토** 아래에서 사용 가능한 옵션을 모두 확장하여 모든 압축 설정이 올바른지 확인합니다. 모두 맞으면 **마침** 을 클릭합니다.  
  
8.  **압축 마법사 진행률** 페이지에서 파티션 작성 마법사의 동작에 대한 상태 정보를 모니터링할 수 있습니다. 마법사에서 선택한 옵션에 따라 진행률 페이지에 하나 이상의 동작이 포함될 수 있습니다. 맨 위에 있는 상자에는 전반적인 마법사 상태와 수신된 상태, 오류 및 경고 메시지의 수가 표시됩니다.  
  
     다음은 **압축 마법사 진행률** 페이지에서 선택할 수 있는 옵션입니다.  
  
     **세부 정보**  
     동작, 상태 및 마법사가 수행한 동작의 결과로 반환된 모든 메시지를 제공합니다.  
  
     **동작**  
     각 동작의 이름과 유형을 지정합니다.  
  
     **상태**  
     마법사 동작 결과 전체적으로 **성공** 값을 반환했는지 또는 **실패** 값을 반환했는지 여부를 나타냅니다.  
  
     **메시지**  
     프로세스에서 반환된 모든 오류 또는 경고 메시지를 제공합니다.  
  
     **Report**  
     파티션 작성 마법사의 결과가 포함된 보고서를 만듭니다. **보고서 보기**, **보고서를 파일로 저장**, **클립보드에 보고서 복사** 및 **보고서를 전자 메일로 보내기** 중에서 선택할 수 있습니다.  
  
     **보고서 보기**  
     파티션 작성 마법사의 진행률에 대한 텍스트 보고서가 포함된 **보고서 보기** 대화 상자를 엽니다.  
  
     **보고서를 파일로 저장**  
     **보고서를 다른 이름으로 저장** 대화 상자를 엽니다.  
  
     **클립보드에 보고서 복사**  
     마법사의 진행률 보고서 결과를 클립보드에 복사합니다.  
  
     **보고서를 전자 메일로 보내기**  
     마법사의 진행률 보고서 결과를 이메일 메시지에 복사합니다.  
  
     완료되면 **닫기** 를 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  

### <a name="sql-server"></a>SQL Server

SQL Server에서 `sp_estimate_data_compression_savings`를 실행한 다음 테이블 또는 인덱스에서 압축을 사용하도록 설정합니다. 다음 섹션을 참조하세요. 

#### <a name="to-enable-compression-on-a-table"></a>테이블에 압축을 사용하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 다음 예에서는 먼저 `sp_estimate_data_compression_savings` 저장 프로시저를 실행하여 ROW 압축 설정을 사용할 경우의 예상 개체 크기를 반환합니다. 그런 다음 지정한 테이블의 모든 파티션에 대해 ROW 압축을 사용하도록 설정합니다.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_estimate_data_compression_savings 'Production', 'TransactionHistory', NULL, NULL, 'ROW' ;  
  
    ALTER TABLE Production.TransactionHistory REBUILD PARTITION = ALL  
    WITH (DATA_COMPRESSION = ROW);   
    GO  
    ```  
  
#### <a name="to-enable-compression-on-an-index"></a>인덱스에 압축을 사용하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 다음 예에서는 먼저 `sys.indexes` 카탈로그 뷰를 쿼리하여 `index_id` 테이블에 있는 각 인덱스의 이름 및 `Production.TransactionHistory` 를 반환합니다. 그런 다음, `sp_estimate_data_compression_savings` 저장 프로시저를 실행하여 PAGE 압축 설정을 사용할 경우의 지정한 인덱스 ID에 대한 예상 크기를 반환합니다. 마지막으로 PAGE 압축을 지정하여 인덱스 ID 2(`IX_TransactionHistory_ProductID`)를 다시 작성합니다.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, index_id  
    FROM sys.indexes  
    WHERE OBJECT_NAME (object_id) = N'TransactionHistory';  
  
    EXEC sp_estimate_data_compression_savings   
        @schema_name = 'Production',   
        @object_name = 'TransactionHistory',  
        @index_id = 2,   
        @partition_number = NULL,   
        @data_compression = 'PAGE' ;   
  
    ALTER INDEX IX_TransactionHistory_ProductID ON Production.TransactionHistory REBUILD PARTITION = ALL WITH (DATA_COMPRESSION = PAGE);  
    GO  
    ``` 
    
### <a name="on-azure-sql-database"></a>Azure SQL Database

Azure SQL Database는 `sp_estimate_data_compression`을 지원하지 않습니다. 다음 스크립트는 압축되는 크기를 추정하지 않고 압축을 사용하도록 설정합니다. 

#### <a name="to-enable-compression-on-a-table"></a>테이블에 압축을 사용하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예제에서는 지정한 테이블의 모든 파티션에 행 압축을 사용하도록 설정합니다.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  

    ALTER TABLE Production.TransactionHistory REBUILD PARTITION = ALL  
    WITH (DATA_COMPRESSION = ROW);   
    GO  
    ```  
  
#### <a name="to-enable-compression-on-an-index"></a>인덱스에 압축을 사용하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 다음 예에서는 먼저 `sys.indexes` 카탈로그 뷰를 쿼리하여 `index_id` 테이블에 있는 각 인덱스의 이름 및 `Production.TransactionHistory` 를 반환합니다. 마지막으로 PAGE 압축을 지정하여 인덱스 ID 2(`IX_TransactionHistory_ProductID`)를 다시 작성합니다.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, index_id  
    FROM sys.indexes  
    WHERE OBJECT_NAME (object_id) = N'TransactionHistory';  
    
    ALTER INDEX IX_TransactionHistory_ProductID ON Production.TransactionHistory REBUILD PARTITION = ALL WITH (DATA_COMPRESSION = PAGE);  
    GO  
    ``` 
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 및 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 압축](../../relational-databases/data-compression/data-compression.md)   
 [sp_estimate_data_compression_savings&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)  
  
  
