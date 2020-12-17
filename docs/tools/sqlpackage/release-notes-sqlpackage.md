---
title: DacFx 및 SqlPackage 릴리스 정보
description: Microsoft sqlpackage에 대한 릴리스 정보입니다.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: cd4fc69334cb9e4bf77a4ccfa4c972d8515bbd1e
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97577976"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe에 대한 릴리스 정보

**[최신 버전 다운로드](sqlpackage-download.md)**

이 문서에는 SqlPackage.exe의 릴리스 버전에서 제공하는 기능 및 수정 사항이 나열되어 있습니다.

## <a name="186-sqlpackage"></a>18.6 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2143544)|2020년 9월 18일|18.6|15.0.4897.1|
|macOS .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2143659)|2020년 9월 18일| 18.6|15.0.4897.1|
|Linux .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2143497)|2020년 9월 18일| 18.6|15.0.4897.1|
|Windows .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2143496)|2020년 9월 18일| 18.6|15.0.4897.1|

### <a name="features"></a>기능
| 기능 | 세부 정보 |
| :------ | :------ |
| 플랫폼 | .NET Core 버전의 sqlpackage를 .NET Core 3.1로 업데이트했습니다. |
| Always Encrypted | SQL Server 2019에서 보안 Enclave 가져오기 및 내보내기 지원을 추가했습니다. |
| 배포 | Azure SQL Database에서 내보낼 때 변경 데이터 캡처 사용 테이블을 무시하는 지원을 추가했습니다. |
| 배포 | Azure SQL Database에서 OPTIMIZE_FOR_SEQUENTIAL_KEY 인덱스 옵션 지원을 추가했습니다. |
| 배포 | Azure Synapse Analytics에 대해 ID 열 지원을 추가했습니다. | 
| 도움말 | 도움말(/?)에 sqlpackage 버전을 출력하고 /version 매개 변수를 지원합니다. | 

### <a name="fixes"></a>수정 프로그램
| 기능 | 세부 정보 |
| :------ | :------ | 
| 배포 | sysadmin이 아닌 사용자로 Azure SQL Managed Instance를 대상으로 지정할 때 생성되는 잘못된 배포 스크립트를 수정했습니다.  | 
| 배포 | 스크립트 작업 실행 시 배포 기여자 로드를 수정했습니다. | 
| 도움말 | 작업이 1일보다 오래 걸리는 경우 sqlpackage에 경과된 시간을 올바르게 출력합니다. | 
| 배포 | .NET Core에 대해 배포 시 dacpac 등록을 수정했습니다. | 
| 배포 | /accessToken(/at) 매개 변수의 .NET Core 처리에 대해 sqlpackage를 수정했습니다. | 
| 배포 | 저장 프로시저의 ALTER TABLE 문을 최상위가 아닌 문으로 허용합니다. | 
| 배포 | 대/소문자를 구분하지 않도록 구체화된 뷰의 Azure Synapse Analytics 유효성 검사를 수정했습니다. | 

### <a name="known-issues"></a>알려진 문제
| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | Azure Synapse Analytics 워크로드 관리 기능(워크로드 그룹 및 워크로드 분류자)은 아직 지원되지 않습니다. | 

## <a name="1851-sqlpackage"></a>18.5.1 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2134206)|2020년 6월 24일|18.5.1|15.0.4826.1|
|macOS .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2134312)|2020년 6월 24일| 18.5.1|15.0.4826.1|
|Linux .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2134311)|2020년 6월 24일| 18.5.1|15.0.4826.1|
|Windows .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2134310)|2020년 6월 24일| 18.5.1|15.0.4826.1|

### <a name="fixes"></a>수정 프로그램
| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | 외부에서 온-프레미스에 로그인한 사용자로 dacpac을 배포하거나 bacpac를 가져올 때 “'형식' 근처의 구문이 잘못되었습니다.” 오류가 발생하는 18.5에서 도입된 회귀 문제가 해결되었습니다. | 

## <a name="185-sqlpackage"></a>18.5 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2128142)|2020년 4월 28일|18.5|15.0.4769.1|
|macOS .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2128145)|2020년 4월 28일| 18.5|15.0.4769.1|
|Linux .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2128144)|2020년 4월 28일| 18.5|15.0.4769.1|
|Windows .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2128143)|2020년 4월 28일| 18.5|15.0.4769.1|

### <a name="features"></a>기능
| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | SQL Server 2008 이상, Azure SQL Database, Azure Synapse Analytics에서 이제 데이터 민감도 분류가 지원됩니다. |
| 배포 | Azure Synapse Analytics에 테이블 제약 조건 지원이 추가되었습니다. |
| 배포 | Azure Synapse Analytics에 순서가 지정된 클러스터형 columnstore 인덱스 지원이 추가되었습니다. |
| 배포 | Oracle, Teradata, MongoDB/CosmosDB, ODBC, Big Data Cluster용 외부 데이터 원본 지원과 SQL Server 2019 Big Data Cluster용 외부 테이블 지원이 추가되었습니다. |
| 배포 | 지원되는 버전으로 SQL Database Edge 인스턴스가 추가되었습니다. |
| 배포 | '\<server>.\<dnszone>.database.windows.net' 형식의 Managed Instance 서버 이름을 지원합니다. |
| 배포 | Azure Synapse Analytics에 복사 명령 지원이 추가되었습니다. |
| 배포 | Azure Synapse Analytics 테이블의 파티션 함수가 변경되었을 때 테이블이 다시 만들어지지 않도록 게시 중에 ‘IgnoreTablePartitionOptions’ 배포 옵션이 추가되었습니다. |
| .NET Core | sqlpackage의 .NET Core 버전에 Microsoft.Data.SqlClient에 대한 지원이 추가되었습니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램
| Fix | 세부 정보 |
| :-- | :------ |
| 배포 | json 경로가 식으로 구문 분석되는 문제가 수정되었습니다. |
| 배포 | AlterAnyDatabaseScopedConfiguration 및 AlterAnySensitivityClassification 권한에 대해 GRANT 문이 생성되는 문제가 수정되었습니다. |
| 배포 | 외부 스크립트 권한이 인식되지 않는 문제가 수정되었습니다. |
| 배포 | 인라인 속성이 수정되었습니다. 속성의 암시적인 추가는 차이에 표시되지 않아야 하나 스크립트를 통해 명시적인 언급이 표시되어야 합니다. |
| 배포 | MV(구체화된 뷰)에서 참조된 테이블을 변경할 경우 Azure Synapse Analytics MV에서 지원되지 않는 Alter View 문이 생성되는 이슈가 해결되었습니다. |
| 배포 | Azure Synapse Analytics 데이터가 있는 테이블에 열을 추가할 경우 게시되지 않는 이슈가 해결되었습니다. |
| 배포 | Azure Synapse Analytics의 배포 열 유형을 변경하는 경우(데이터 손실 시나리오) 데이터를 새 테이블로 이동하도록 업데이트 스크립트가 수정되었습니다. |
| ScriptDom | 인라인 인덱스 뒤에 정의된 인라인 제약 조건을 인식하지 않는 ScriptDom 버그가 수정되었습니다. |
| ScriptDom | 일괄 처리 문에서 ScriptDom SYSTEM_TIME에 닫는 괄호가 누락된 문제가 수정되었습니다. |
| Always Encrypted | sqlpackage가 다시 연결되었는데 연결이 끊기면 임시 테이블이 사라지므로 임시 테이블이 이미 사라진 경우 #tmpErrors 테이블이 삭제되지 않는 문제가 수정되었습니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제
| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 |  외부에서 온-프레미스에 로그인한 사용자로 dacpac을 배포하거나 bacpac를 가져올 때 “'형식' 근처의 구문이 잘못되었습니다.” 오류가 발생하는 회귀 문제가 18.5에서 도입되었습니다. 해결 방법은 sqlpackage 18.4를 사용하는 것입니다. 이 문제는 다음 sqlpackage 릴리스에서 수정될 예정입니다. | 
| .NET Core | Microsoft.Data.SqlClient에서 이 [알려진 문제](https://github.com/dotnet/SqlClient/issues/559) 때문에 민감도 분류가 포함된 bacpac 가져오기가 "심각한 내부 연결 오류"와 함께 실패합니다. 이 문제는 다음 sqlpackage 릴리스에서 수정될 예정입니다. |
| &nbsp; | &nbsp; |

## <a name="1841-sqlpackage"></a>18.4.1 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2113703)|2019년 12월 13일|18.4.1|15.0.4630.1|
|macOS .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2113705)|2019년 12월 13일| 18.4.1|15.0.4630.1|
|Linux .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2113331)|2019년 12월 13일| 18.4.1|15.0.4630.1|
|Windows .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2113704)|2019년 12월 13일| 18.4.1|15.0.4630.1|

### <a name="fixes"></a>수정 프로그램
| Fix | 세부 정보 |
| :-- | :------ |
| ScriptDom |  ScriptDom 구문 분석 회귀는 'RENAME'이 최상위 토큰으로 잘못 처리되어 구문 분석이 실패하는 18.3.1에서 도입되었습니다.
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제 

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 |  18.4.1에서 외부 로그인을 사용하는 사용자가 있는 dacpac을 배포하거나 bacpac을 가져올 때 “개체 참조가 개체의 인스턴스로 설정되지 않았습니다” 오류를 발생시키는 회귀가 발생했습니다. 해결 방법은 sqlpackage 18.4를 사용하는 것입니다. 이 문제는 다음 sqlpackage 릴리스에서 수정될 예정입니다. | 
| &nbsp; | &nbsp; |

## <a name="184-sqlpackage"></a>18.4 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2108813)|2019년 10월 29일|18.4|15.0.4573.2|
|macOS .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2108815)|2019년 10월 29일| 18.4|15.0.4573.2|
|Linux .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2108814)|2019년 10월 29일| 18.4|15.0.4573.2|
|Windows .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2109019)|2019년 10월 29일| 18.4|15.0.4573.2|

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | Azure Synapse Analytics(GA)에 배포할 지원이 추가되었습니다. | 
| 플랫폼 | macOS, Linux 및 Windows용 sqlpackage .NET Core GA. | 
| 보안 | SHA1 코드 서명을 제거합니다. |
| 배포 | 새 Azure 데이터베이스 버전에 대한 지원을 추가합니다. GeneralPurpose, BusinessCritical, Hyperscale |
| 배포 | Azure Active Directory 사용자 및 그룹에 대한 Managed Instance 지원을 추가합니다. |
| 배포 | .NET Core에서 sqlpackage에 대한 /AccessToken 매개 변수를 지원합니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제 

| 기능 | 세부 정보 |
| :------ | :------ |
| ScriptDom |  ScriptDom 구문 분석 회귀는 'RENAME'이 최상위 토큰으로 잘못 처리되어 구문 분석이 실패하는 18.3.1에서 도입되었습니다. 이 문제는 다음 sqlpackage 릴리스에서 수정될 예정입니다. | 
| &nbsp; | &nbsp; |

### <a name="known-issues-for-net-core"></a>.NET Core에 대한 알려진 문제

| 기능 | 세부 정보 |
| :------ | :------ |
| 가져오기 |  크기가 4GB를 초과하는 압축 파일이 포함된 .bacpac 파일의 경우 sqlpackage의 .NET Core 버전을 사용하여 가져오기를 수행해야 할 수 있습니다.  이 동작은 .NET Core가 sqlpackage의 .NET Full Framework 버전에서 사용할 수 없는 zip 헤더를 생성하는 방식 때문입니다. | 
| 배포 | /p:Storage=File 매개 변수는 지원되지 않습니다. 메모리만 .NET Core에서 지원됩니다. | 
| Always Encrypted | sqlpackage .NET Core는 Always Encrypted 열을 지원하지 않습니다. | 
| 보안 | sqlpackage .NET Core는 다단계 인증에 대한 /ua 매개 변수를 지원하지 않습니다. | 
| 배포 | Json 데이터 serialization을 사용하는 이전 V2 .dacpac 및.bacpac 파일이 지원되지 않습니다. |
| &nbsp; | &nbsp; |

## <a name="1831-sqlpackage"></a>18.3.1 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2102893)|2019년 9월 13일|18.3.1|15.0.4538.1|
|macOS .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2102894)|2019년 9월 13일| 18.3.1|15.0.4538.1|
|Linux .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2102978)|2019년 9월 13일| 18.3.1|15.0.4538.1|
|Windows .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2102979)|2019년 9월 13일| 18.13.1|15.0.4538.1|

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | Azure Synapse Analytics(미리 보기)에 배포할 지원이 추가되었습니다. | 
| 배포 | sqlpackage에 /p:DatabaseLockTimeout=(INT32 '60') 매개 변수를 추가합니다. | 
| 배포 | sqlpackage에 /p:LongRunningCommandTimeout=(INT32) 매개 변수를 추가합니다. |
| 내보내기/추출 | sqlpackage에 /p:TempDirectoryForTableData=(STRING) 매개 변수를 추가합니다. |
| 배포 | 배포 참가자가 추가 위치에서 로드될 수 있도록 허용합니다. 배포 참가자는 배포되는 대상 .dacpac과 동일한 디렉터리, sqlpackage.exe 이진 파일에 상대적인 Extensions 디렉터리, 추가 디렉터리 위치를 지정할 수 있는 sqlpackage에 추가된 /p:AdditionalDeploymentContributorPaths=(STRING) 매개 변수에서 로드됩니다. |
| 배포 | OPTIMIZE_FOR_SEQUENTIAL_KEY에 대한 지원을 추가합니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 배포 | 배포 시 삭제되지 않게 자동 인덱스를 무시하도록 수정합니다. | 
| Always Encrypted | Always Encrypted varchar 열 처리를 수정합니다. | 
| 빌드/배포 | xml 열 집합에 대한 nodes() 메서드를 해결하도록 수정합니다.| 
| ScriptDom | 'URL' 문자열이 최상위 토큰으로 해석된 추가 사례를 수정합니다. | 
| 그래프 | 제약 조건에서 의사 열 참조에 대해 생성된 TSQL을 수정합니다.  | 
| 내보내기 | 복잡성 요구 사항을 충족하는 임의 암호를 생성합니다. | 
| 배포 | 제약 조건을 검색할 때 명령 제한 시간을 적용하도록 수정합니다. | 
| .NET Core(미리 보기) | 파일에 대한 진단 로깅을 수정합니다. | 
| .NET Core(미리 보기) | 대용량 테이블을 지원하기 위해 스트리밍을 사용하여 테이블 데이터를 내보냅니다. | 
| &nbsp; | &nbsp; |

## <a name="182-sqlpackage"></a>18.2 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2087429)|2019년 4월 15일|18.2|15.0.4384.2|
|macOS .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2087247)|2019년 4월 15일 | 18.2 |15.0.4384.2|
|Linux .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2087431)|2019년 4월 15일 | 18.2 |15.0.4384.2|

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 그래프 | 에지 제약 조건 및 에지 제약 조건 절에 대한 그래프 테이블 지원을 추가합니다. |
| 배포 | SQL Server 2016 이상의 인덱스 키에 대해 32개 열을 지원하도록 모델 유효성 검사 규칙을 사용하도록 설정했습니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 배포 | 사용 중인 지원되지 않은 쿼리 힌트로 인한 SQL Server 2016 RTM 데이터베이스 리버스 엔지니어링을 수정합니다. |
| 배포 | create filegroup 문을 만들기 전에 발생하도록 auto close alter 문의 배포 순서를 수정합니다. |
| ScriptDom | 'URL' 문자열이 최상위 토큰으로 해석된 ScriptDom 구문 분석 회귀를 수정합니다. |
| 배포 | alter table add index 문을 구문 분석할 때 null 참조 예외를 수정합니다. | 
| 스키마 비교 | 항상 다른 것으로 표시되는 nullable 지속형 계산 열의 스키마 비교를 수정했습니다.|
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>18.1 sqlpackage

릴리스 날짜: &nbsp; 2019년 2월 1일  
빌드: &nbsp; 15.0.4316.1  
미리 보기 릴리스입니다.

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | UTF8 데이터 정렬에 대한 지원을 추가했습니다. |
| 배포 | 인덱싱된 뷰에서 비클러스터형 columnstore 인덱스를 사용하도록 설정했습니다. |
| 플랫폼 | .NET Core 2.2로 이동했습니다. | 
| 스키마 비교 | .NET Core에서 스키마 비교에 메모리 기반 스토리지를 사용합니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 성능 | 리버스 엔지니어링 쿼리에 레거시 카디널리티 평가기를 사용하기 위한 성능 수정입니다. | 
| 성능 | 스크립트를 생성할 때 중요한 스키마 비교 성능 문제를 수정했습니다. | 
| 스키마 비교 | 특정 확장 이벤트(xevent) 세션을 무시하도록 스키마 드리프트 검색 논리를 수정했습니다. |
| 그래프 | 그래프 테이블의 가져오기 순서를 수정했습니다. | 
| 내보내기 | 개체 권한과 함께 외부 테이블 내보내기를 수정했습니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

이 릴리스에는 .NET Core 2.2를 대상으로 하는 sqlpackage의 플랫폼 간 미리 보기 빌드가 포함됩니다. sqlpackage는 macOS 및 Linux에서 실행할 수 있습니다.

| 알려진 문제 | 세부 정보 |
| :---------- | :------ |
| 배포 | .NET Core에서는 빌드 및 배포 참가자가 지원되지 않습니다. | 
| 배포 | .NET Core에서는 Json 데이터 serialization을 사용하는 이전 .dacpac 및.bacpac 파일이 지원되지 않습니다. | 
| 배포 | .NET Core에서는 대/소문자 구분 파일 시스템 문제로 인해 참조된.dacpacs(예: master.dacpac)를 확인할 수 없습니다. | 이 문제를 해결하려면 참조 파일의 이름을 대문자로 바꿉니다(예: MASTER.BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

릴리스 날짜: &nbsp; 2018년 10월 24일  
빌드: &nbsp; 15.0.4200.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | 데이터베이스 호환성 수준 150에 대한 지원을 추가했습니다. | 
| 배포 | Managed Instance에 대한 지원을 추가했습니다. | 
| 성능 | 데이터베이스 작업의 병렬 처리 수준을 지정하는 MaxParallelism 명령줄 매개 변수를 추가했습니다. | 
| 보안 | SQL Server에 연결할 때 인증 토큰을 지정하는 AccessToken 명령줄 매개 변수를 추가했습니다. | 
| 가져오기 | 가져오기에 대한 BLOB/CLOB 데이터 형식을 스트리밍하도록 지원을 추가했습니다. | 
| 배포 | 스칼라 UDF 'INLINE' 옵션에 대한 지원을 추가했습니다. | 
| 그래프 | 그래프 테이블의 'MERGE' 구문에 대한 지원을 추가했습니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 그래프 | 그래프 테이블에 대한 확인되지 않은 의사(pseudo) 열을 수정했습니다. |
| 배포 | 메모리 최적화 테이블이 사용되는 경우 메모리 최적화 파일 그룹이 포함된 데이터베이스 만들기를 수정했습니다. |
| 배포 | 외부 테이블에 확장 속성 포함을 수정했습니다. |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

릴리스 날짜: &nbsp; June 22, 2018  
빌드: &nbsp; 14.0.4079.2

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 진단 | SqlClient 예외 메시지를 포함하여 연결 실패의 오류 메시지를 향상했습니다. |
| 배포 | 가져오기/내보내기를 위해 단일 파티션 인덱스에서 인덱스 압축을 지원합니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 배포 | SQL 2017 이상에서 XML 열 집합의 리버스 엔지니어링 문제를 수정했습니다. | 
| 배포 | Azure SQL Database에서 데이터베이스 호환성 수준 140 스크립팅이 무시된 문제를 수정했습니다. |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

릴리스 날짜: &nbsp; 2018년 1월 25일  
빌드: &nbsp; 14.0.3917.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 가져오기/내보내기 | 많은 수의 중첩 문이 있는 Transact-SQL을 구문 분석하는 ThreadMaxStackSize 명령줄 매개 변수를 추가했습니다. |
| 배포 | 데이터베이스 카탈로그 데이터 정렬 지원입니다. | 
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 가져오기 | Azure SQL Database .bacpac를 온-프레미스 인스턴스로 가져올 때 _이 버전의 SQL Server에서는 암호가 없는 데이터베이스 마스터 키가 지원되지 않습니다_ 로 인한 오류를 수정했습니다. |
| 그래프 | 그래프 테이블에 대한 확인되지 않은 의사(pseudo) 열 오류를 수정했습니다. |
| 스키마 비교 | 스키마를 비교하는 SQL 인증을 수정했습니다. | 
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

릴리스 날짜: &nbsp; 2017년 12월 12일  
빌드: &nbsp; 14.0.3881.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 |  SQL 2017 이상 및 Azure SQL Database에서 ‘임시 보존 정책’에 대한 지원을  추가했습니다. | 
| 진단 | 진단 정보를 저장할 파일 경로를 지정하는 /DiagnosticsFile:"C:\Temp\sqlpackage.log" 명령줄 매개 변수를 추가했습니다. | 
| 진단 | 진단 정보를 콘솔에 기록하는 /Diagnostics 명령줄 매개 변수를 추가했습니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 배포 | 인식할 수 없는 데이터베이스 호환성 수준이 발생하는 경우 차단하지 않습니다. 대신 최신 Azure SQL Database 또는 온-프레미스 플랫폼이 간주됩니다. |
| &nbsp; | &nbsp; |
