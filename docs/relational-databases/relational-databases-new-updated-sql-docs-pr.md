---
title: "업데이트 됨-관계형 데이터베이스 docs | Microsoft Docs"
description: "가져온 조각을 관계형 데이터베이스에 대 한 최근에 변경 된 설명서에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 3ab051a6fd00670139bb1089dcd3f4af76b9ecef
ms.contentlocale: ko-kr
ms.lasthandoff: 06/23/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>신규 / 최근에 업데이트: 관계형 데이터베이스 docs



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-05-01** &nbsp; 을 아래와 같이 &nbsp; **2017-05-23**
- *주제 영역:* &nbsp; **관계형 데이터베이스**합니다.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>부분 업데이트 되는 문서

이 섹션에는 최근에 발견 된 대규모 업데이트를 문서에서 수집 하는 업데이트의 발췌 한 내용 표시 됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sqlgraphssql-graph-samplemd"></a>1. &nbsp;[그래프 데이터베이스를 만들고 일부 패턴 일치 T-SQL을 사용 하 여 쿼리를 실행 합니다.](graphs/sql-graph-sample.md)

*Updated: 2017-05-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 68.  ms.author= "shkale".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ff467bf5fcf13592c796836def36e16e34f8cc31 99fcf0399006de16d0ac7cc9057564d307cb981b -->


```
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table, 
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 1), 
       (SELECT $node_id FROM Restaurant WHERE id = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 2), 
      (SELECT $node_id FROM Restaurant WHERE id = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 3), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 4), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 5), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 1),
      (SELECT $node_id FROM City WHERE id = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 2),
      (SELECT $node_id FROM City WHERE id = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 3),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 4),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 5),
      (SELECT $node_id FROM City WHERE id = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 1),
      (SELECT $node_id FROM City WHERE id =1));
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sysfngetauditfile-transact-sqlsystem-functionssys-fn-get-audit-file-transact-sqlmd"></a>2. &nbsp; [sys.fn_get_audit_file (TRANSACT-SQL)](system-functions/sys-fn-get-audit-file-transact-sql.md)

*Updated: 2017-05-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 046fa92ad1b7e6bb7a956493ca06cf72d45b5285 fbf55361da90663835d7e107fda697c358e0e061 -->



- **Azure SQL Database***

  다음 예에서는 이름이 `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`인 파일에서 읽습니다.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  이 예제에서는 모든 감사 로그가로 시작 하는 서버에서 읽고 `Sh`합니다.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```





&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd"></a>3. &nbsp;[시스템 버전 임시 테이블에서 기록 데이터의 보존 관리](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b -->



**임시 기록 보존 정책 접근 방식 사용**

> **참고:** 임시 기록 보존 정책을 사용 하 여 접근 방식을 적용 [! INCLUDE [sqldbesa... /.. /includes/sqldbesa-md.md)] 및 SQL Server 2017 CTP 1.3에서 시작 합니다.  

임시 기록 보존 될 수 있습니다 정책은 사용자가을 유연한 에이징을 만들 수 있는 개별 테이블 수준에서 구성 합니다. 임시 보존이 적용 하는 것은 간단: 테이블 스키마를 만들거나 변경 하는 동안 설정 하려면 매개 변수는 하나만 필요 합니다.

보존 정책을 정의 하 고 나면 Azure SQL 데이터베이스는 자동 데이터 정리에 사용할 수 있는 기록 행이 있는 경우 정기적으로 검사를 시작 합니다. 일치 하는 행 식별 하 고 기록 테이블에서 해당 제거 예약 되 고 시스템에서 실행 하는 백그라운드 태스크에서 투명 하 게 발생 합니다. 기록 테이블의 행에 대 한 나이 조건은 나타내는 SYSTEM_TIME 기간 종료 열에 따라 확인 됩니다. 예를 들어 보존 기간 이후 6 개월으로 설정 된, 경우 테이블의 정리에 대 한 적격 행 다음 조건을 만족 합니다.
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
앞의 예제에서 ValidTo 열 SYSTEM_TIME 기간 종료에 해당 하는지을 가정 합니다.
**보존 정책을 구성 하려면 어떻게 하나요?**

데이터베이스 수준에서 임시 기록 보존이 사용 되는지 여부를 임시 테이블에 대 한 보존 정책을 구성 하기 전에 먼저 검사.
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
플래그 데이터베이스 **is_temporal_history_retention_enabled** 기본적으로 ON으로 설정 되어 사용자가 ALTER DATABASE 문을 사용 하 여 변경할 수 있습니다. 시간 복원 작업에서 이후에 자동으로 OFF로 설정 됩니다. 데이터베이스에 대 한 임시 기록 보존 정리를 활성화 하려면 다음 문을 실행 합니다.
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
보존 정책은 HISTORY_RETENTION_PERIOD 매개 변수 값을 지정 하 여 테이블을 만들 때 구성 됩니다.
```
CREATE TABLE dbo.WebsiteUserInfo
```





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact를 최근에 업데이트 하는 문서 목록

이 압축 목록 이전 섹션에 나열 된 모든 업데이트 된 문서에 대 한 링크를 제공 합니다.

1. [그래프 데이터베이스를 만들고 일부 패턴 일치 T-SQL을 사용 하 여 쿼리를 실행 합니다.](#TitleNum_1)
2. [sys.fn_get_audit_file (TRANSACT-SQL)](#TitleNum_2)
3. [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](#TitleNum_3)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>대체 문서

이 섹션 동일한 GitHub 리포지토리 내에서 다른 주제 영역에서 최근에 업데이트 된 아티클에 대 한 매우 유사한 문서를 나열합니다.


&nbsp;

[Microsoft /**sql-docs pr** ](https://github.com/microsoftdocs/sql-docs-pr/) GitHub.com에 리포지토리:

- [최근 업데이트: **관계형 데이터베이스 및 Microsoft SQL Server** docs](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [최근 업데이트: **Microsoft SQL Server** docs](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [최근 업데이트: **SQL Server에서 TRANSACT-SQL** docs](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



