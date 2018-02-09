---
title: "업데이트-SQL Server 문서에 대 한 고급 분석 | Microsoft Docs"
description: "코드 조각에 최근에 변경 된 설명서, Microsoft SQL Server에 대 한 고급 분석에 대 한 업데이트 된 콘텐츠를 표시 합니다."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 02/03/2018
ms.openlocfilehash: a0c31eb21282cc876b34fc1c9d4b3e697f2c7213
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>새로 추가 되거나 최근에 업데이트 된: SQL Server에 대 한 고급 분석



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-12-03** &nbsp; 을 아래와 같이 &nbsp; **2018-02-03**
- *주제 영역:* &nbsp; **SQL Server에 대 한 고급 분석**합니다.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 기사

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server에 새로운 Python 패키지 설치](python/install-additional-python-packages-on-sql-server.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>부분 업데이트 되는 문서

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact를 최근에 업데이트 하는 문서 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [컴퓨터 학습 서비스의 알려진된 문제](#TitleNum_1)
2. [데이터베이스에서 실행에 대 한 R 코드 변환](#TitleNum_2)
3. [R 패키지는 SQL Server에 설치 된 확인](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1. &nbsp;[컴퓨터 학습 서비스의 알려진 문제](known-issues-for-sql-server-machine-learning-services.md)

*업데이트 됨된: 2018-02-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([다음](#TitleNum_2))

<!-- Source markdown line 163.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c6f46adcf795c43f818120b88407a3a89304cb27 c781562605f5cd77f6c43bfe5e89810cb72ceae0  (PR=4789  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=386bfb688843bac7fa4d83dc1cfef94dd19db110) -->



R 솔루션에 영향을 줄 수 있는 기타 알려진된 문제에 대 한 참조는 [컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/resources-known-issues) 사이트입니다.

**기본이 아닌 위치에서 SQL Server에서 R 스크립트를 실행 하는 경우 경고를 거부 하는 액세스**


와 같은 기본이 아닌 위치에 설치 된 SQL Server 인스턴스의 경우 외부에서 `Program Files` 폴더에는 경고 ACCESS_DENIED가 패키지를 설치 하는 스크립트를 실행 하려고 할 때 발생 합니다. 예를 들어

> *In normalizePath(path.expand(path), winslash, mustWork) : path[2]="~ExternalLibraries/R/8/1": Access is denied*

R 함수는 경로 읽으려고 시도 및 실패 이유는 기본 제공 users 그룹 **SQLRUserGroup**, 읽기 권한이 없습니다. 경고 발생 하는 현재 R 스크립트 실행을 차단 하지 않습니다 되지만 사용자는 다른 R 스크립트를 실행할 때마다 경고가 반복적으로 되풀이 수 있습니다.

SQL Server의 기본 위치에 설치한 경우이 오류가 발생 하지 않습니다, 모든 Windows 사용자 읽기 권한이에 있어야 하기 때문에 `Program Files` 폴더입니다.

이 문제는 향후 서비스 릴리스에서 해결 될 예정입니다. 이 문제를 해결 제공 그룹 **SQLRUserGroup**의 모든 상위 폴더에 대 한 읽기 권한이 있는 `ExternalLibraries`합니다.

**RevoScaleR의 이전 및 새 버전 간 serialization 오류**


원격 SQL Server 인스턴스를 serialize 된 형식을 사용 하 여 모델을 전달 하면 오류가 발생할 수 있습니다.

> *MemDecompress의 오류 (데이터, 유형 = 압축을 풀) memDecompress(2) 내부 오류-3입니다.*

최신 버전의 serialization 함수를 사용 하 여 모델을 저장 한 경우이 오류는 발생 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), 모델을 역직렬화 하는 SQL Server 인스턴스는 이전 버전의 SQL에서 RevoScaleR Api에는 있지만 서버 2017 CU2 또는 이전 버전입니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-converting-r-code-for-execution-in-databaserconverting-r-code-for-use-in-sql-servermd"></a>2. &nbsp;[데이터베이스에서 실행에 대 한 변환 R 코드](r/converting-r-code-for-use-in-sql-server.md)

*업데이트 됨된: 2018-01-08* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 136.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a1d156fac1af5813ef75965071686b177e2aede7 fc8beff0aa0d7ea298e493b90984875e81e9143e  (PR=4493  ,  Filename=converting-r-code-for-use-in-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f486d12078a45c87b0fcf52270b904ca7b0c7fc8) -->



**저장된 프로시저에서 R 코드**

+ 코드 비교적 단순한 경우 이러한 예제에 설명 된 대로 수정 하지 않고 T-SQL 사용자 정의 함수에 포함할 수 있습니다.

    + [RxExec에서 실행 되는 R 함수 만들기](r/../tutorials/deepdive-create-a-simple-simulation.md)
    + [T-SQL과 R을 사용 하 여 기능 엔지니어링](r/../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 보다 복잡 한 코드의 경우 R 패키지를 사용 하 여 **sqlrutils** 코드를 변환할 수 있습니다. 이 패키지는 숙련 된 R 사용자가 좋은 저장된 프로시저 코드를 작성할 수 있도록 설계 되었습니다.

    R 코드를 명확 하 게 정의 된 입력 및 출력으로 단일 함수로 다시 작성 하는 첫 번째 단계가입니다.

    그런 다음 사용 하는 **sqlrutils** 올바른 형식으로 입력 및 출력을 생성 하는 패키지입니다. **sqlrutils** 패키지 완전 한 저장된 프로시저 코드가 자동으로 생성 및 저장된 프로시저는 데이터베이스에 등록할 수도 있습니다.

    자세한 내용 및 예제에 대 한 참조 [SqlRUtils](r/../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)합니다.

**다른 워크플로와 통합**

+ T-SQL 도구 및 ETL 프로세스를 활용 합니다. 기능 엔지니어링, 기능 추출 및 데이터 워크플로의 일부로 데이터 사전에 정리를 수행 합니다.

    Visual Studio 또는 RStudio R 도구와 같은 전용된 R 개발 환경에서 작업 하는 수를 컴퓨터에 데이터를 가져올를 반복적으로 데이터를 분석 및 다음 작성 또는 결과 표시 합니다.

    그러나 패키지가 마이그레이션되면 독립 실행형 R 코드는 SQL Server로 대부분이 프로세스의 수 수 간소화 되거나 다른 SQL Server 도구에 위임 합니다.

+ 안전 하 고 비동기 시각화 전략을 사용 합니다.

    SQL Server의 사용자를 종종는 서버에서 파일에 액세스할 수 없습니다 및 SQL 클라이언트 도구는 R 그래픽 장치를 일반적으로 지원 하지 않습니다. 솔루션의 일부로 점도 또는 다른 그래픽을 생성 하는 경우는 점도 이진 데이터로 내보내는 및를 테이블에 저장 또는 쓰는 것이 좋습니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3. &nbsp;[는 R 패키지는 SQL Server에 설치 된 확인](r/determine-which-packages-are-installed-on-sql-server.md)

*업데이트 됨된: 2018-01-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_2))

<!-- Source markdown line 78.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9a065066398843a4bed318fa46d4982d712915a9 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f  (PR=4715  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=9e6a029456f4a8daddb396bc45d7874a43a47b45) -->




**가져오기 라이브러리 위치 및 버전**


다음 예제에서는 로컬 계산 컨텍스트 및 패키지 버전에서 RevoScaleR의 라이브러리 위치를 가져옵니다.

```
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

**SQL Server에서 사용 되는 라이브러리의 경로 확인 합니다.**


기계 학습 바인딩을 사용 하 여 구성 요소를 업그레이드 한 경우 경로 R 라이브러리를 변경할 수 있습니다. 이 경우 이전의 바로 가기가 R 도구를 이전 버전을 참조할 수 있습니다. 하도록 하려면 SQL Server에서 사용 하는 경로 패키지 버전의 다음과 같은 명령을 실행할 수 있습니다.

```
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**결과**

```
STDOUT message(s) from external script:
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```







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


