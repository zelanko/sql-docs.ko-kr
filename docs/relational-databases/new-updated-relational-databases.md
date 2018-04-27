---
title: 업데이트됨 - 관계형 데이터베이스 문서 | Microsoft Docs
description: 관계형 데이터베이스 설명서에서 최근에 변경된 업데이트된 콘텐츠의 일부를 표시합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: relational-databases
ms.date: 02/03/2018
ms.openlocfilehash: fc37abbb88aa597a6173fa5579fa320e0024581f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>새로 추가되었거나 최근에 업데이트됨: 관계형 데이터베이스 문서



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-12-03** &nbsp;부터 &nbsp; **2018-02-03**까지
- *주제 영역:* &nbsp; **관계형 데이터베이스**




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server 또는 SQL Database에 JSON 문서 저장](json/store-json-documents-in-sql-tables.md)
2. [SQL 취약성 평가](security/sql-vulnerability-assessment.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [데이터베이스 파일 초기화](#TitleNum_1)
2. [tempdb 데이터베이스](#TitleNum_2)
3. [SQL Server의 JSON 데이터](#TitleNum_3)
4. [1단원: 데이터베이스 엔진에 연결](#TitleNum_4)
5. [트랜잭션 로그 파일의 크기 관리](#TitleNum_5)
6. [bcp_bind](#TitleNum_6)
7. [SQL Server 인덱스 디자인 가이드](#TitleNum_7)
8. [sp_execute_external_script(Transact-SQL)](#TitleNum_8)
9. [기본 키 만들기](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-database-file-initializationdatabasesdatabase-instant-file-initializationmd"></a>1. &nbsp; [데이터베이스 파일 초기화](databases/database-instant-file-initialization.md)

*업데이트됨: 2018-01-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 81.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5f2aa53a8b43d4c43e0602cf945cb7c7028a27d 04c261c6588af1f53cda2fce3e9a86167c50b686  (PR=4702  ,  Filename=database-instant-file-initialization.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=3206a31870f8febab7d1718fa59fe0590d4d45db) -->



```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**적용 대상:** SQL Server(SQL Server 2012 SP4, SQL Server 2014 SP2 및 SQL Server 2016부터 SQL Server 2017까지)

**Security Considerations**

삭제된 디스크 내용은 새 데이터가 파일에 기록될 때만 덮어쓰기 때문에 인스턴트 파일 초기화(IFI)를 사용하는 경우 데이터 파일의 해당하는 특정 영역에 다른 데이터를 쓸 때까지 권한 없는 사용자가 삭제된 내용에 액세스할 수 있습니다. 데이터베이스 파일이 SQL Server의 인스턴스에 연결되어 있는 동안 파일의 DACL(임의 액세스 제어 목록)에 의해 이러한 정보 공개 위험이 줄어듭니다. 이 DACL은 SQL Server 서비스 계정 및 로컬 관리자에게만 파일 액세스를 허용합니다. 그러나 파일이 분리되면 SE\_MANAGE\_VOLUME_NAME이 없는 사용자 또는 서비스가 액세스할 수 있습니다. 데이터베이스를 백업할 때도 유사한 사항을 고려해야 합니다. 즉, 백업 파일이 적절한 DACL로 보호되지 않는 경우 권한이 없는 사용자 또는 서비스가 삭제된 내용을 사용할 수 있게 됩니다.

또 다른 고려 사항은 파일이 IFI를 사용하여 증가하는 경우입니다. SQL Server 관리자는 잠재적으로 원시 페이지 콘텐츠에 엑세스하고 이전에 삭제된 내용을 확인할 수 있습니다.

데이터베이스 파일을 저장 영역 네트워크에서 호스트하는 경우 저장 영역 네트워크는 항상 미리 초기화된 새 페이지를 표시하고 운영 체제에서 페이지를 다시 초기화하는 경우 불필요한 오버헤드가 발생할 수 있습니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>2. &nbsp; [tempdb 데이터베이스](databases/tempdb-database.md)

*업데이트됨: 2018-01-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 100.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d 3257c92d6e2a88968fc44e5f6262c02cd0624635  (PR=0  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



 이러한 데이터베이스 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션(Transact-SQL)](databases/../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.

**SQL Database의 Tempdb 데이터베이스**


|SLO|최대 Tempdb 데이터 파일 크기(MB)|tempdb 데이터 파일 수|최대 tempdb 데이터 크기(MB)|
|---|---:|---:|---:|
|Basic|14,225|1|14,225|
|S0|14,225|1|14,225|
|S1|14,225|1|14,225|
|S2|14,225| 1|14,225|
|S3|32,768|1|32,768|
|S4|32,768|2|65,536|
|S6|32,768|3|98,304|
|S7|32,768|6|196,608|
|S9|32,768|12|393,216|
|S12|32,768|12|393,216|
|P1|32,768|12|393,216|
|P2|32,768|12|393,216|
|P4|32,768|12|393,216|
|P6|32,768|12|393,216|
|P11|32,768|12|393,216|
|P15|32,768|12|393,216|
|프리미엄 탄력적 풀(모든 DTU 구성)|14,225|12|170,700|
|표준 탄력적 풀(모든 DTU 구성)|14,225|12|170,700|
|기본 탄력적 풀(모든 DTU 구성)|14,225|12|170,700|
||||




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>3. &nbsp; [SQL Server의 JSON 데이터](json/json-data-sql-server.md)

*업데이트됨: 2018-02-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_2) | [다음](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 62dd9c68d8cb72d6bf51b941a0731224514f0a7f 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5  (PR=4783  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=73f18ae24a9a48234bf997ee9a2ef441bc4918b9) -->



-   [SQL Server 2016으로 GeoJSON 데이터 로드](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/)

**SQL 쿼리를 사용하여 JSON 데이터 분석**

보고를 위해 JSON 데이터를 필터링하거나 집계해야 하는 경우 **OPENJSON**을 사용하여 JSON을 관계형 형식으로 변환할 수 있습니다. 그런 다음, 표준 Transact-SQL 및 기본 제공 함수를 사용하여 보고서를 작성할 수 있습니다.

```
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM   SalesOrderRecord AS Tab
          CROSS APPLY
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')
           WITH (
              Number   varchar(200) N'$.Order.Number',
              Date     datetime     N'$.Order.Date',
              Customer varchar(200) N'$.AccountNumber',
              Quantity int          N'$.Item.Quantity'
           )
  AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-lesson-1-connecting-to-the-database-enginelesson-1-connecting-to-the-database-enginemd"></a>4. &nbsp; [1단원: 데이터베이스 엔진에 연결](lesson-1-connecting-to-the-database-engine.md)

*업데이트됨: 2017-12-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_3) | [다음](#TitleNum_5))

<!-- Source markdown line 79.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c070935895450fd2ea054e2be9e1c48f7dc2b6c 0c386e3d47fb7f8f1e63b9301f0cafec2bc88ab0  (PR=4282  ,  Filename=lesson-1-connecting-to-the-database-engine.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=6e016a4ffd28b09456008f40ff88aef3d911c7ba) -->



2.  **데이터베이스 엔진**을 선택합니다.

    ![object-explorer](../relational-databases/media/object-explorer.png)

3.  **서버 이름** 상자에 데이터베이스 엔진 인스턴스의 이름을 입력합니다. 기본 SQL Server 인스턴스의 경우 서버 이름은 컴퓨터 이름입니다. SQL Server의 명명된 인스턴스의 경우 서버 이름은 *<computer_name>***\\***<instance_name>,*(예: **ACCTG_SRVR\SQLEXPRESS**)입니다. 다음 스크린샷은 'PracticeComputer' 컴퓨터에 있는 SQL Server의 기본(명명되지 않은) 인스턴스에 연결하는 방법을 보여 줍니다. Windows에 로그인한 사용자는 Contoso 도메인의 Mary입니다. Windows 인증을 사용하는 경우 사용자 이름을 변경할 수 없습니다.

    ![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  **연결**을 클릭합니다.

> [!NOTE]
> 이 자습서에서는 여러분이 SQL Server 를 처음 사용하며 특별한 연결 문제가 없다고 가정합니다. 그러면 대부분의 사용자를 수용하고 이 자습서를 단순하게 유지할 수 있습니다. 자세한 문제 해결 단계는 [SQL Server 데이터베이스 엔진에 대한 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)을 참조하세요.

**<a name="additional"></a>추가 연결 권한 부여**

SQL Server에 관리자로 연결한 다음 가장 먼저 수행해야 할 태스크 중 하나는 다른 사용자가 연결할 수 있도록 권한을 부여하는 것입니다. 로그인을 만들고 이 로그인이 사용자로서 데이터베이스에 액세스할 수 있도록 권한을 부여하여 이 작업을 수행합니다. 로그인은 Windows 자격 증명을 사용하는 Windows 인증 로그인이나 SQL Server에 인증 정보를 저장하며 Windows 자격 증명과는 독립적인 SQL Server 인증 로그인 중 하나일 수 있습니다. 가능하면 Windows 인증을 사용하십시오.



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-manage-the-size-of-the-transaction-log-filelogsmanage-the-size-of-the-transaction-log-filemd"></a>5. &nbsp; [트랜잭션 로그 파일의 크기 관리](logs/manage-the-size-of-the-transaction-log-file.md)

*업데이트됨: 2018-01-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_4) | [다음](#TitleNum_6))

<!-- Source markdown line 105.  ms.author= "jhubbard".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5847b31cf8f6003a380f0c8aaa289efdc55be678 84e45320d81db218cde17fbf8b9668a9ac3805a7  (PR=0  ,  Filename=manage-the-size-of-the-transaction-log-file.md  ,  Dirpath=docs\relational-databases\logs\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



-   작은 확장 증분은 너무 많은 [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)가 생성되어 성능이 저하될 수 있습니다. 주어진 인스턴스의 모든 데이터베이스의 현재 트랜잭션 로그 크기에 대한 최적의 VLF 분포 및 필수 크기를 수행할 필수 성장 증분을 결정하려면 이 [스크립트](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)를 참조하세요.

-   큰 확장 증분은 너무 적고 큰 [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)가 생성되어 이 또한 성능에 영향을 줄 수 있습니다. 주어진 인스턴스의 모든 데이터베이스의 현재 트랜잭션 로그 크기에 대한 최적의 VLF 분포 및 필수 크기를 수행할 필수 성장 증분을 결정하려면 이 [스크립트](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)를 참조하세요.

-   자동 증가를 사용하는 경우에도 쿼리의 요구 사항을 충족시킬 정도로 빠르게 커질 수 없는 경우 트랜잭션 로그가 꽉 찼다는 메시지를 받을 수 있습니다. 확장 증분 변경에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41; 파일 및 파일 그룹 옵션](logs/../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.

-   트랜잭션 로그 파일이 동일한 파일 그룹의 데이터 파일처럼 [비례 채우기](logs/../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill)를 사용하지 않기 때문에 데이터베이스에 여러 로그 파일을 저장해도 성능이 향상되지 않습니다.

-   로그 파일은 자동으로 축소되도록 설정할 수 있습니다. 그러나 이것은 **권장되지 않으며** **auto_shrink** 데이터베이스 속성은 기본적으로 FALSE로 설정됩니다. **auto_shrink**를 TRUE로 설정하면 파일 공간의 25% 이상이 사용되지 않을 때만 자동 축소에 의해 파일 크기가 줄어듭니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-bcpbindnative-client-odbc-extensions-bulk-copy-functionsbcp-bindmd"></a>6. &nbsp; [bcp_bind](native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)

*업데이트됨: 2018-01-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_5) | [다음](#TitleNum_7))

<!-- Source markdown line 127.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d50791cef948ce8b3066438e317ab4d34d535258 e6f70559e7237cfc86dfc5746d218c08bec52af6  (PR=4762  ,  Filename=bcp-bind.md  ,  Dirpath=docs\relational-databases\native-client-odbc-extensions-bulk-copy-functions\  ,  MergeCommitSha40=60006e90d03fdb75b282bbc0dad3d40571bacacc) -->



 다음 표에는 유효한 열거형 데이터 형식 및 해당 ODBC C 데이터 형식이 나열되어 있습니다.

|eDataType|C 형식|
|-----------------------|------------|
|SQLTEXT|char *|
|SQLNTEXT|wchar_t *|
|SQLCHARACTER|char *|
|SQLBIGCHAR|char *|
|SQLVARCHAR|char *|
|SQLBIGVARCHAR|char *|
|SQLNCHAR|wchar_t *|
|SQLNVARCHAR|wchar_t *|
|SQLBINARY|unsigned char *|
|SQLBIGBINARY|unsigned char *|
|SQLVARBINARY|unsigned char *|
|SQLBIGVARBINARY|unsigned char *|
|SQLBIT|char|
|SQLBITN|char|
|SQLINT1|char|
|SQLINT2|short int|
|SQLINT4|ssNoversion|
|SQLINT8|_int64|
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|
|SQLFLT4|FLOAT|
|SQLFLT8|FLOAT|
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|
|SQLDECIMALN|SQL_NUMERIC_STRUCT|
|SQLNUMERICN|SQL_NUMERIC_STRUCT|
|SQLMONEY|DBMONEY|
|SQLMONEY4|DBMONEY4|
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|
|SQLTIMEN|SQL_SS_TIME2_STRUCT|
|SQLDATEN|SQL_DATE_STRUCT|
|SQLDATETIM4|DBDATETIM4|
|SQLDATETIME|DBDATETIME|
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|
|SQLIMAGE|unsigned char *|
|SQLUDT|unsigned char *|
|SQLUNIQUEID|SQLGUID|
|SQLVARIANT|*다음을 제외한 모든 데이터 형식:*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|
|SQLXML|*지원되는 C 데이터 형식:*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-sql-server-index-design-guidesql-server-index-design-guidemd"></a>7. &nbsp; [SQL Server 인덱스 디자인 가이드](sql-server-index-design-guide.md)

*업데이트됨: 2018-01-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_6) | [다음](#TitleNum_8))

<!-- Source markdown line 700.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bd09c9e66cd3cf5f3ebebe7ffa6e937978353169 8e5cbbf0063971676a8bafefba75aa5c7c28be61  (PR=0  ,  Filename=sql-server-index-design-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=74daee358fef75a25d75c69d971d08536c5bd2be) -->



SQL Server 2016부터 **rowstore 테이블에서 업데이트 가능한 비클러스터형 columnstore 인덱스를 만들 수 있습니다**. columnstore 인덱스는 데이터 복사본을 저장하므로 추가 저장소가 필요합니다. 그러나 columnstore 인덱스의 데이터는 rowstore 테이블보다 작은 크기로 압축됩니다.  따라서 columnstore 인덱스에서 분석을 실행하고 이와 동시에 rowstore 인덱스에서 트랜잭션을 실행할 수 있습니다. rowstore 테이블의 데이터가 변경되면 columnstore가 업데이트되므로 두 인덱스 모두 동일한 데이터에 대해 작동합니다.

SQL Server 2016부터 **하나의 클러스터형 columnstore 인덱스에서 하나 이상의 비클러스터형 rowstore 인덱스를 사용할 수 있습니다**. 따라서 기본 columnstore에서 효율적인 테이블 찾기를 수행할 수 있습니다. 다른 옵션도 사용할 수 있습니다. 예를 들어 rowstore 테이블에서 UNIQUE 제약 조건을 사용하여 기본 키 제약 조건을 적용할 수 있습니다. 고유하지 않은 값은 rowstore 테이블에 삽입하지 못하므로 SQL Server에서 columnstore에 값을 삽입할 수 없습니다.

**성능 고려 사항**


-   비클러스터형 columnstore 인덱스 정의는 필터링된 조건 사용을 지원합니다. OLTP 테이블에 columnstore 인덱스를 추가할 경우 성능에 미치는 영향을 최소화하려면 필터링된 조건을 사용하여 운영 워크로드의 콜드 데이터에 대해서만 비클러스터형 columnstore 인덱스를 만듭니다.

-   메모리 내 테이블에는 columnstore 인덱스가 한 개만 있을 수 있습니다. 테이블을 만들 때 이 인덱스를 만들거나 나중에 [ALTER TABLE&#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md)을 사용하여 추가할 수 있습니다. SQL Server 2016 전에는 디스크 기반 테이블만 columnstore 인덱스를 사용할 수 있었습니다.

자세한 내용은 [Columnstore 인덱스 - 쿼리 성능](../relational-databases/indexes/columnstore-indexes-query-performance.md)을 참조하세요.

**디자인 지침**


-   Rowstore 테이블에는 업데이트할 수 있는 비클러스터형 columnstore 인덱스 한 개가 있을 수 있습니다. SQL Server 2014 전에는 비클러스터형 columnstore 인덱스가 읽기 전용이었습니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-spexecuteexternalscript-transact-sqlsystem-stored-proceduressp-execute-external-script-transact-sqlmd"></a>8. &nbsp; [sp_execute_external_script(Transact-SQL)](system-stored-procedures/sp-execute-external-script-transact-sql.md)

*업데이트됨: 2018-01-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_7) | [다음](#TitleNum_9))

<!-- Source markdown line 207.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0ee4d591ae9d9a5c015eec98aad9ccbb86268761 ac9b439c23ffae5fcc77639de6ff955763cf5844  (PR=4696  ,  Filename=sp-execute-external-script-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=d7dcbcebbf416298f838a39dd5de6a46ca9f77aa) -->



Python을 사용하여 비슷한 모델을 생성하려면 언어 식별자를 `@language=N'R'`에서 `@language = N'Python'`으로 변경하고 `@script` 인수를 필요한 대로 수정합니다. 그렇지 않으면 모든 매개 변수가 R과 똑같이 작동합니다.

**C. Python 모델을 만들고 거기서 점수 생성**


이 예제에서는 sp\_execute\_external\_script를 사용하여 간단한 Python 모델에서 점수를 생성하는 방법을 보여줍니다.

```
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

**Input query to generate the customer data**

DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders`

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

**Get data from input query**

customer_data = my_input_data

**Define the model**

n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Python 코드에 사용된 열 머리글은 SQL Server로 출력되지 않으므로 WITH RESULTS 문을 사용하여 사용할 SQL의 열 이름과 데이터 형식을 지정합니다.

점수 매기기의 경우 네이티브 [PREDICT](system-stored-procedures/../../t-sql/queries/predict-transact-sql.md) 함수를 사용할 수도 있으며, 이 함수는 Python 또는 R 런타임 호출을 방지하기 때문에 일반적으로 더 빠릅니다.




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-create-primary-keystablescreate-primary-keysmd"></a>9. &nbsp; [기본 키 만들기](tables/create-primary-keys.md)

*업데이트됨: 2018-01-18* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_8))

<!-- Source markdown line 102.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d18b485f314cc005d624cab8a51650d3b8f55f89 9bd2e9453206e8940d30b0a01c43f9d8e1aed606  (PR=4652  ,  Filename=create-primary-keys.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**비클러스터형 인덱스를 사용하여 새 테이블에 기본 키를 만들려면**


1.  **개체 탐색기**에서 데이터베이스 엔진의 인스턴스에 연결합니다.

2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.

3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 테이블을 만들고 `CustomerID` 열에 기본 키를, `TransactionID` 열에 클러스터형 인덱스를 정의합니다.

```
    USE AdventureWorks2012;
    GO
    CREATE TABLE Production.TransactionHistoryArchive1
    (
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)
    );
    GO

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
```







## <a name="similar-articles-about-new-or-updated-articles"></a>신규 문서 또는 업데이트된 문서에 대한 유사 문서

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *있는* 주제 영역


- [새로 추가되었거나 업데이트됨(1+3):&nbsp; **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(12+1): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(6+2):&nbsp; **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(15+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(2+9):&nbsp; **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(1+0):&nbsp; **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **SQL Operations
 Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+2):&nbsp; **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2):&nbsp; **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역


- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../samples/new-updated-samples.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


