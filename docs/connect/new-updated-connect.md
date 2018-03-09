---
title: "SQL Server 문서에 연결 업데이트 됨-| Microsoft Docs"
description: "코드 조각에 최근에 변경 된 설명서, Microsoft SQL Server에 연결에 대 한 업데이트 된 콘텐츠를 표시 합니다."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: connect
ms.date: 02/03/2018
ms.openlocfilehash: cc4eb05dc4dcd74623c8ce7dfa7b7842449d79b6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>새로 추가 되거나 최근에 업데이트 된: SQL Server에 연결



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-12-03** &nbsp; 을 아래와 같이 &nbsp; **2018-02-03**
- *주제 영역:* &nbsp; **SQL Server에 연결**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 기사

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


***지금은 나열할 새 문서가 없습니다.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>부분 업데이트 되는 문서

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact를 최근에 업데이트 하는 문서 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [SQL Server 용 ODBC 드라이버와 함께 상시 암호화 사용](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-using-always-encrypted-with-the-odbc-driver-for-sql-serverodbcusing-always-encrypted-with-the-odbc-drivermd"></a>1. &nbsp;[For SQL Server ODBC 드라이버를 사용 하 여 항상 암호화를 사용 하 여](odbc/using-always-encrypted-with-the-odbc-driver.md)

*업데이트 됨된: 2018-01-22* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 524.  ms.author= "v-chojas".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a52abae2a8f27c3b5bc411ef758610116a608f9f 352368eb269b98ab5ca3a9791fae2e70bf26277a  (PR=4686  ,  Filename=using-always-encrypted-with-the-odbc-driver.md  ,  Dirpath=docs\connect\odbc\  ,  MergeCommitSha40=82c9868b5bf95e5b0c68137ba434ddd37fc61072) -->



**SQLGetData 사용 하 여 파트에서 데이터 검색**

SQL Server 용 ODBC 드라이버 17 암호화 전에 SQLGetData 사용 하 여 파트의 문자 및 이진 열을 검색할 수 없습니다. SQLGetData 한 번만 호출 전체 열의 데이터를 포함 하기에 충분 한 길이의 버퍼에 수행할 수 있습니다.

**SQLPutData 사용 하 여 파트에 데이터 보내기**

SQLPutData 사용 하 여 파트의 삽입 또는 비교에 대 한 데이터를 보낼 수 없습니다. 전체 데이터를 포함 하는 버퍼에 SQLPutData 한 번만 호출을 수행할 수 있습니다. 암호화 된 열에 대 한 long 데이터를 삽입에 대 한 입력된 데이터 파일을 사용한 다음 섹션에 설명 된 대량 복사 API를 사용 합니다.

**암호화 된 money 및 smallmoney**

암호화 **money** 또는 **smallmoney** 매개 변수에서 열을 대상으로 지정할 수, ODBC 데이터 형식 피연산자 유형 충돌 오류가 발생 하는 형식에 매핑하는 더 특정 있기 때문입니다.

**암호화 된 열에 대량 복사**


사용은 [SQL 대량 복사 함수](odbc/../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) 및 **bcp** 유틸리티 SQL Server 용 ODBC 드라이버 17 이후 상시 암호화와 함께 지원 됩니다. 일반 텍스트 (에서 암호화 된 삽입 및에서 해독 된 검색) 및 (정확 하 게 전송 된) 암호 텍스트를 둘 다 삽입 될 수 있습니다 및 대량 복사 (bcp_ *) Api를 사용 하 여 검색 및 **bcp** 유틸리티입니다.

- Varbinary (max) 형식 (예: 대량 로드를 위한 다른 데이터베이스로) 암호 텍스트를 검색, 없이 연결는 `ColumnEncryption` 옵션 (이 속성을 설정 하거나 `Disabled`) BCP OUT 작업을 수행 합니다.

- 삽입 및 일반 텍스트를 검색 한 암호화 및 암호 해독 필요한 설정으로 투명 하 게 수행 하는 드라이버를 사용 하 `ColumnEncryption` 를 `Enabled` 충분 합니다. 그렇지 않으면 BCP API의 기능 변경 되지 않습니다.

- varbinary (max) 형식 (예: 검색 됨 위에) 암호 텍스트를 삽입, 설정 된 `BCPMODIFYENCRYPTED` TRUE 하려면 옵션을 선택 하 고 BCP IN 작업을 수행 합니다. 결과 데이터를 해독할 수에 대 한 순서로 대상 열의 CEK 인지 확인 암호 텍스트를 원래 가져온와 동일 합니다.







## <a name="similar-articles-about-new-or-updated-articles"></a>신규 또는 업데이트 된 문서에 대 한 유사한 문서

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>주제 영역은 *않습니다* 새로 추가 되거나 최근에 업데이트 문서


- [새 + 업데이트 (1 + 3):&nbsp; **SQL에 대 한 고급 분석** docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [새 + 업데이트 (0 + 1):&nbsp; **SQL에 대 한 분석 플랫폼 시스템** docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새 + 업데이트 (0 + 1):&nbsp; **SQL에 연결** docs](../connect/new-updated-connect.md)
- [새 + 업데이트 (0 + 1):&nbsp; **SQL에 대 한 데이터베이스 엔진** docs](../database-engine/new-updated-database-engine.md)
- [새 + 업데이트 (12 + 1): **sql Integration Services** docs](../integration-services/new-updated-integration-services.md)
- [새 + 업데이트 (6 + 2):&nbsp; **SQL에 대 한 Linux** docs](../linux/new-updated-linux.md)
- [새 + 업데이트 (15 + 0): **SQL에 대 한 PowerShell** docs](../powershell/new-updated-powershell.md)
- [새 + 업데이트 (2 + 9):&nbsp; **SQL에 대 한 관계형 데이터베이스** docs](../relational-databases/new-updated-relational-databases.md)
- [새 + 업데이트 (1 + 0):&nbsp; **sql Reporting Services** docs](../reporting-services/new-updated-reporting-services.md)
- [새 + 업데이트 (1 + 1):&nbsp; **SQL 작업 Studio** docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새 + 업데이트 (1 + 1):&nbsp; **Microsoft SQL Server** docs](../sql-server/new-updated-sql-server.md)
- [새 + 업데이트 (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** docs](../ssdt/new-updated-ssdt.md)
- [새 + 업데이트 (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** docs](../ssms/new-updated-ssms.md)
- [새 + 업데이트 (0 + 2):&nbsp; **TRANSACT-SQL** docs](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>영역을 수행 하는 주체 *하지* 가 새로 추가 되거나 최근에 업데이트 문서


- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새 + 업데이트 (0 + 0): **ADO ActiveX Data Objects ()에 대 한 SQL** docs](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 데이터 품질 서비스** docs](../data-quality-services/new-updated-data-quality-services.md)
- [새 + 업데이트 (0 + 0): **확장 DMX (Data Mining) sql** docs](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새 + 업데이트 (0 + 0): **MDX (Multidimensional Expressions)에 대 한 SQL** docs](../mdx/new-updated-mdx.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 ODBC (Open Database Connectivity)** docs](../odbc/new-updated-odbc.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 샘플** docs](../sample/new-updated-sample.md)
- [새 + 업데이트 (0 + 0): **SQL Server Migration Assistant (SSMA)** docs](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 XQuery** docs](../xquery/new-updated-xquery.md)


