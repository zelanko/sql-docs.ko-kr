---
title: 전체 텍스트 인덱스 채우기 | Microsoft 문서
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d6f871fabba547268736dca990215b89ae84e9eb
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011174"
---
# <a name="populate-full-text-indexes"></a>전체 텍스트 인덱스 채우기
  전체 텍스트 인덱스를 만들고 유지 관리하려면 *채우기* ( *탐색*이라고도 함)라는 프로세스를 사용하여 인덱스를 채워야 합니다.  
  
##  <a name="types"></a> 채우기 유형  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 유형의 채우기 지원 합니다: 전체 채우기, 변경 내용 추적 기반 자동 또는 수동 채우기 및 증분 타임 스탬프 기반 채우기입니다.  
  
### <a name="full-population"></a>전체 채우기  
 전체 채우기 중에는 테이블 또는 인덱싱된 뷰의 모든 행에 대해 인덱스 항목이 작성됩니다. 전체 텍스트 인덱스의 전체 채우기는 기본 테이블 또는 인덱싱된 뷰의 모든 행에 대해 인덱스 항목을 작성합니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 새 전체 텍스트 인덱스를 만드는 즉시 채웁니다. 그러나 전체 채우기는 많은 양의 리소스를 사용할 수 있습니다. 따라서 리소스 사용량이 많을 때 전체 텍스트 인덱스를 만들 경우, 특히 전체 텍스트 인덱스의 기본 테이블이 클 경우 리소스 사용량이 많지 않을 때까지 전체 채우기를 지연시키는 것이 좋습니다. 그러나 인덱스가 속한 전체 텍스트 카탈로그는 전체 텍스트 인덱스가 모두 채워질 때까지 사용할 수 없습니다. 전체 텍스트 인덱스를 즉시 채우지 않고 만들려면 CREATE FULLTEXT INDEX 문에 CHANGE_TRACKING OFF, NO POPULATION 절을 지정합니다. CHANGE_TRACKING MANUAL을 지정하면 전체 텍스트 엔진에서 문을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 START FULL POPULATION 또는 START INCREMENTAL POPULATION 절을 사용 하 여 ALTER FULLTEXT INDEX 문을 실행할 때까지 새로운 전체 텍스트 인덱스를 채우지 않습니다 됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 예 "1. 전체 채우기를 실행하지 않고 전체 텍스트 인덱스 만들기" 및 "2. 테이블에 대해 전체 채우기 실행"을 참조하십시오.  
  

  
### <a name="change-tracking-based-population"></a>변경 내용 추적 기반 채우기  
 경우에 따라 초기 전체 채우기 후에 변경 내용 추적을 사용하여 전체 텍스트 인덱스를 유지 관리할 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 마지막 채우기 후에 기본 테이블의 변경 내용을 추적하는 테이블을 유지 관리하기 때문에 변경 내용 추적을 사용할 경우 약간의 오버헤드가 발생합니다. 변경 내용 추적을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업데이트, 삭제 또는 삽입에 의해 수정된 기본 테이블 또는 인덱싱된 뷰의 행 레코드를 유지 관리합니다. WRITETEXT 및 UPDATETEXT를 통한 데이터 변경 내용은 전체 텍스트 인덱스에 반영되지 않고 변경 내용 추적 시 선택되지도 않습니다.  
  
> [!NOTE]  
>  `timestamp` 열이 포함된 테이블에 대해서는 증분 채우기를 사용할 수 있습니다.  
  
 인덱스를 만드는 동안 변경 내용 추적을 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 새 전체 텍스트 인덱스를 만드는 즉시 완전히 채웁니다. 그 이후에는 변경 내용이 추적되고 전체 텍스트 인덱스로 전파됩니다. 변경 내용 추적에는 두 가지 유형, 자동(CHANGE_TRACKING AUTO 옵션)과 수동(CHANGE_TRACKING MANUAL 옵션)이 있습니다. 자동 변경 내용 추적이 기본 동작입니다.  
  
 변경 내용 추적의 유형에 따라 전체 텍스트 인덱스가 채워지는 방법이 다음과 같이 결정됩니다.  
  
-   자동 채우기  
  
     기본적으로 또는 CHANGE_TRACKING AUTO를 지정한 경우 전체 텍스트 엔진은 전체 텍스트 인덱스에 대해 자동 채우기를 사용합니다. 초기 전체 채우기가 완료된 후 기본 테이블의 데이터가 수정되면 변경 내용이 추적되고 추적된 변경 내용이 자동으로 전파됩니다. 그러나 전체 텍스트 인덱스가 백그라운드에서 업데이트되기 때문에 전파된 변경 내용은 인덱스에 즉시 반영되지 않을 수도 있습니다.  
  
     **자동 채우기를 사용 하 여 변경 내용 추적을 설정 하려면**  
  
    -   [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... SET CHANGE_TRACKING AUTO  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 예 "5. 자동 변경 내용 추적을 사용하도록 전체 텍스트 인덱스 변경"을 참조하십시오.  
  
-   수동 채우기  
  
     CHANGE_TRACKING MANUAL을 지정한 경우 전체 텍스트 엔진에서는 전체 텍스트 인덱스에 대해 수동 채우기를 사용합니다. 초기 전체 채우기가 완료된 후 기본 테이블의 데이터가 수정되면 변경 내용이 추적됩니다. 그러나 추적된 변경 내용은 ALTER FULLTEXT INDEX…를 실행할 때까지 전체 텍스트 인덱스로 전파되지 않습니다. START UPDATE POPULATION 문을 사용하여 수동으로 변경 내용을 적용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 주기적으로 호출할 수 있습니다.  
  
     **수동 채우기가 있는 변경 내용 추적을 시작하려면**  
  
    -   [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... SET CHANGE_TRACKING MANUAL  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 예 "3. 수동 변경 내용 추적이 있는 전체 텍스트 인덱스 만들기" 및 "4. 수동 채우기 실행"을 참조하십시오.  
  
 **변경 내용 추적을 해제 하려면**  
  
-   [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... SET CHANGE_TRACKING OFF  
  

  
### <a name="incremental-timestamp-based-population"></a>증분 타임스탬프 기반 채우기  
 증분 채우기는 전체 텍스트 인덱스를 수동으로 채우는 대체 메커니즘으로, CHANGE_TRACKING이 MANUAL 또는 OFF로 설정된 전체 텍스트 인덱스에 대해 실행할 수 있습니다. 전체 텍스트 인덱스에 대해 처음으로 실행하는 채우기가 증분 채우기이면 모든 행이 인덱싱되므로 그 결과가 전체 채우기의 경우와 같습니다.  
  
 증분 채우기를 사용하려면 인덱싱된 테이블에 `timestamp` 데이터 형식의 열이 있어야 합니다. `timestamp` 열이 없으면 증분 채우기를 수행할 수 없습니다. `timestamp` 열이 없는 테이블에 대해 증분 채우기를 요청하면 전체 채우기 작업이 수행됩니다. 또한 테이블의 전체 텍스트 인덱스에 영향을 주는 메타데이터가 마지막 채우기 후에 변경된 경우 증분 채우기 요청은 전체 채우기로 구현됩니다. 여기에는 열, 인덱스 또는 전체 텍스트 인덱스 정의의 변경으로 인한 메타데이터 변경 내용이 포함됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 `timestamp` 열을 사용하여 마지막 채우기 후에 변경된 행을 식별합니다. 그러면 증분 채우기는 마지막 채우기 후 또는 마지막 채우기를 진행 중인 동안 추가, 삭제 또는 수정된 행에 대해 전체 텍스트 인덱스를 업데이트합니다. 테이블에서 대량 삽입이 발생하는 경우 증분 채우기를 사용하는 것이 수동 채우기를 사용하는 것보다 효율적일 수 있습니다.  
  
 채우기 완료 시 전체 텍스트 엔진은 새 `timestamp` 값을 기록합니다. 이 값은 SQL Gatherer에서 발생한 가장 큰 `timestamp` 값입니다. 이 값은 후속 증분 채우기가 시작될 때 사용됩니다.  
  
 증분 채우기를 실행하려면 START INCREMENTAL POPULATION 절을 사용하여 ALTER FULLTEXT INDEX 문을 실행합니다.  
  

  
##  <a name="examples"></a> 전체 텍스트 인덱스 채우기의 예  
  
> [!NOTE]  
>  이 섹션의 예에서는 `Production.Document` 예제 데이터베이스의 `HumanResources.JobCandidate` 또는 `AdventureWorks` 테이블을 사용합니다.  
  
### <a name="a-creating-a-full-text-index-without-running-a-full-population"></a>1. 전체 채우기를 실행하지 않고 전체 텍스트 인덱스 만들기  
 다음 예에서는 `Production.Document` 예제 데이터베이스의 `AdventureWorks` 테이블에서 전체 텍스트 인덱스를 만듭니다. 이 예에서는 WITH CHANGE_TRACKING OFF, NO POPULATION을 사용하여 초기 전체 채우기를 지연시킵니다.  
  
```  
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="b-running-a-full-population-on-table"></a>2. 테이블에 대해 전체 채우기 실행  
 다음 예에서는 `Production.Document` 예제 데이터베이스의 `AdventureWorks` 테이블에 대해 전체 채우기를 실행합니다.  
  
```  
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
  
### <a name="c-creating-a-full-text-index-with-manual-change-tracking"></a>3. 수동 변경 내용 추적이 있는 전체 텍스트 인덱스 만들기  
 다음 예에서는 `HumanResources.JobCandidate` 예제 데이터베이스의 `AdventureWorks` 테이블에 대해 수동 채우기가 있는 변경 내용 추적을 사용하는 전체 텍스트 인덱스를 만듭니다.  
  
```  
USE AdventureWorks;  
GO  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH CHANGE_TRACKING=MANUAL;  
GO  
```  
  
### <a name="d-running-a-manual-population"></a>4. 수동 채우기 실행  
 다음 예에서는 `HumanResources.JobCandidate` 예제 데이터베이스의 `AdventureWorks` 테이블에서 변경 내용 추적이 설정된 전체 텍스트 인덱스에 대해 수동 채우기를 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
GO  
```  
  
### <a name="e-altering-a-full-text-index-to-use-automatic-change-tracking"></a>5. 자동 변경 내용 추적을 사용하도록 전체 텍스트 인덱스 변경  
 다음 예에서는 자동 채우기와 함께 변경 내용 추적을 사용하도록 `HumanResources.JobCandidate` 예제 데이터베이스의 `AdventureWorks` 테이블에 대한 전체 텍스트 인덱스를 변경합니다.  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
GO   
```  
  

  
##  <a name="create"></a> 만들기 또는 증분 채우기 일정을 변경 합니다.  
  
#### <a name="to-create-or-change-a-schedule-for-incremental-population-in-management-studio"></a>Management Studio에서 증분 채우기 일정을 만들거나 변경하려면  
  
1.  개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 전체 텍스트 인덱스가 포함된 데이터베이스를 확장합니다.  
  
3.  **테이블**을 확장합니다.  
  
 전체 텍스트 인덱스가 정의된 테이블을 마우스 오른쪽 단추로 클릭하고 **전체 텍스트 인덱스**를 선택한 다음 **전체 텍스트 인덱스** 상황에 맞는 메뉴에서 **속성**을 클릭합니다. 그러면 **전체 텍스트 인덱스 속성** 대화 상자가 열립니다.  
  
1.  **페이지 선택** 창에서 일정을 선택합니다.  
  
     이 페이지를 사용하여 전체 텍스트 인덱스의 기본 테이블 또는 인덱싱된 뷰에 대한 증분 테이블 채우기를 시작하는 SQL Server 에이전트 작업의 일정을 만들거나 관리할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  기본 테이블이나 뷰에 `timestamp` 데이터 형식의 열이 포함되어 있지 않으면 전체 채우기가 수행됩니다.  
  
     다음과 같은 옵션이 있습니다.  
  
    -   새 일정을 만들려면 **새로 만들기**를 클릭합니다.  
  
         그러면 일정을 만들 수 있는 **새 전체 텍스트 인덱싱 테이블 일정** 대화 상자가 열립니다. 일정을 저장하려면 **확인**을 클릭합니다.  
  
        > [!IMPORTANT]  
        >  **전체 텍스트 인덱스 속성** 대화 상자를 닫으면 SQL Server 에이전트 작업(*database_name*.*table_name*에 대한 증분 테이블 채우기 시작)이 새 일정에 연결됩니다. 전체 텍스트 인덱스 일정을 여러 개 만들 경우 모두 동일한 작업을 사용합니다.  
  
    -   일정을 변경하려면 일정을 선택하고 **편집**을 클릭합니다.  
  
         그러면 일정을 수정할 수 있는 **새 전체 텍스트 인덱싱 테이블 일정** 대화 상자가 열립니다.  
  
        > [!NOTE]  
        >  작업을 수정하는 방법은 [작업 수정](../../ssms/agent/modify-a-job.md)을 참조하세요.  
  
    -   일정을 제거하려면 일정을 선택하고 **삭제**를 클릭합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  

  
##  <a name="crawl"></a> 전체 텍스트 채우기 (탐색) 오류 문제 해결  
 탐색 중에 오류가 발생하면 전체 텍스트 검색 탐색 로깅 기능은 일반 텍스트 파일인 탐색 로그를 만들고 유지 관리합니다. 각 탐색 로그는 특정 전체 텍스트 카탈로그에 해당합니다. 이 경우 지정된 된 인스턴스에 대해 기본 크롤링 로그에서이 첫 번째 인스턴스를 %ProgramFiles%\Microsoft SQL Server\MSSQL12에에서 있습니다. MSSQLSERVER\MSSQL\LOG 폴더입니다. 탐색 로그 파일은 다음 명명 구성표를 따릅니다.  
  
 SQLFT\<DatabaseID>\<FullTextCatalogID>.LOG[\<n>]  
  
 <`DatabaseID`>  
 데이터베이스의 ID입니다. <`dbid`>는 5 자리 숫자 앞에 오는 0입니다.  
  
 <`FullTextCatalogID`>  
 전체 텍스트 카탈로그 ID입니다. <`catid`>는 5 자리 숫자 앞에 오는 0입니다.  
  
 <`n`>  
 동일한 전체 텍스트 카탈로그의 탐색 로그가 하나 이상 있음을 나타내는 정수입니다.  
  
 예를 들어 SQLFT0000500008.2는 데이터베이스 ID = 5, 전체 텍스트 카탈로그 ID = 8인 데이터베이스의 탐색 로그 파일입니다. 파일 이름 끝에 있는 2는 이 데이터베이스/카탈로그 쌍의 탐색 로그 파일이 두 개 있음을 나타냅니다.  
  

  
## <a name="see-also"></a>관련 항목  
 [sys.dm_fts_index_population&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)   
 [전체 텍스트 검색 시작](get-started-with-full-text-search.md)   
 [전체 텍스트 인덱스 만들기 및 관리](create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
