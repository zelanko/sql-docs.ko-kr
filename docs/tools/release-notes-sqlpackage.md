---
title: DacFx 및 SqlPackage 릴리스 정보 | Microsoft Docs
description: Microsoft sqlpackage에 대한 릴리스 정보입니다.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 11e10f4a29b15efbd2b0ee513080a2000ae7e2f1
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033046"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe에 대한 릴리스 정보

**[최신 버전 다운로드](sqlpackage-download.md)**

이 문서에는 SqlPackage.exe의 릴리스 버전에서 제공하는 기능 및 수정 사항이 나열되어 있습니다.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="184-sqlpackage"></a>18.4 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전 옵션|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2108813)|2019년 10월 29일|18.4|15.0.4573.2|
|macOS .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2108815)|2019년 10월 29일| 18.4|15.0.4573.2|
|Linux .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2108814)|2019년 10월 29일| 18.4|15.0.4573.2|
|Windows .NET Core |[zip 파일](https://go.microsoft.com/fwlink/?linkid=2109019)|2019년 10월 29일| 18.4|15.0.4573.2|

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | Azure SQL Data Warehouse에 배포할 수 있도록 지원 (GA)을 추가 합니다. | 
| 플랫폼 | macOS, Linux 및 Windows 용 .NET Core GA를 sqlpackage. | 
| 보안 | SHA1 코드 서명을 제거 합니다. |
| 배포 | 새 Azure 데이터베이스 버전에 대 한 지원 추가: 일반 용도, BusinessCritical, Hyperscale |
| 배포 | AAD 사용자 및 그룹에 대 한 Managed Instance 지원을 추가 합니다. |
| 배포 | .NET Core의 sqlpackage에 대 한/AccessToken 매개 변수를 지원 합니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제 

| 기능 | 세부 정보 |
| :------ | :------ |
| ScriptDom |  ScriptDom 구문 분석 회귀는 ' RENAME '이 최상위 토큰으로 잘못 처리 되어 구문 분석이 실패 하는 18.3.1에서 도입 되었습니다. 이 문제는 다음 sqlpackage 릴리스에서 수정 될 예정입니다. | 
| &nbsp; | &nbsp; |

### <a name="known-issues-for-net-core"></a>.NET Core에 대 한 알려진 문제

| 기능 | 세부 정보 |
| :------ | :------ |
| 가져오기 |  크기가 4GB를 초과 하는 압축 파일이 포함 된 bacpac 파일의 경우 sqlpackage의 .NET Core 버전을 사용 하 여 가져오기를 수행 해야 할 수 있습니다.  이 동작은 .net Core가 sqlpackage의 .NET 전체 프레임 워크 버전에서 사용할 수 없는 zip 헤더를 생성 하는 방법 때문에 발생 합니다. | 
| 배포 | 매개 변수/p: Storage = File은 지원 되지 않습니다. .NET Core 에서만 메모리를 사용할 수 있습니다. | 
| Always Encrypted | sqlpackage .NET Core는 Always Encrypted 열을 지원 하지 않습니다. | 
| 보안 | sqlpackage .NET Core는 multi-factor authentication에 대해/sera 매개 변수를 지원 하지 않습니다. | 
| 배포 | Json 데이터 serialization을 사용하는 이전 V2 .dacpac 및.bacpac 파일이 지원되지 않습니다. |
| &nbsp; | &nbsp; |

## <a name="1831-sqlpackage"></a>18.3.1 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전 옵션|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2102893)|2019년 9월 13일|18.3.1|15.0.4538.1|
|macOS .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2102894)|2019년 9월 13일| 18.3.1|15.0.4538.1|
|Linux .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2102978)|2019년 9월 13일| 18.3.1|15.0.4538.1|
|Windows .NET Core (미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2102979)|2019년 9월 13일| 18.13.1|15.0.4538.1|

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 배포 | Azure SQL Data Warehouse (미리 보기)에 배포할 지원을 추가 합니다. | 
| 배포 | Sqlpackage에/p: DatabaseLockTimeout = (INT32 ' 60 ') 매개 변수를 추가 합니다. | 
| 배포 | Sqlpackage에/p: LongRunningCommandTimeout = (INT32) 매개 변수를 추가 합니다. |
| 내보내기/추출 | Sqlpackage에/p: TempDirectoryForTableData = (STRING) 매개 변수를 추가 합니다. |
| 배포 | 배포 참가자가 추가 위치에서 로드 될 수 있도록 허용 합니다. 배포 참가자는 배포 되는 대상으로 동일한 디렉터리에서 로드 되며, sqlpackage 바이너리에 상대적인 확장 디렉터리와 sqlpackage에 추가 된/p: AdditionalDeploymentContributorPaths = (STRING) 매개 변수입니다. 추가 디렉터리 위치를 지정할 수 있습니다. |
| 배포 | OPTIMIZE_FOR_SEQUENTIAL_KEY에 대 한 지원을 추가 합니다. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 배포 | 자동 인덱스를 무시 하 여 배포 시 삭제 되지 않도록 수정 합니다. | 
| Always Encrypted | Always Encrypted varchar 열 처리를 수정 합니다. | 
| 빌드/배포 | Xml 열 집합에 대 한 nodes () 메서드를 해결 하려면 수정 합니다.| 
| ScriptDom | ' URL ' 문자열이 최상위 토큰으로 해석 된 추가 사례를 수정 합니다. | 
| 그래프 | 제약 조건에서 의사 열 참조에 대해 생성 된 TSQL을 수정 합니다.  | 
| 내보내기 | 복잡성 요구 사항을 충족 하는 임의의 암호를 생성 합니다. | 
| 배포 | 제약 조건을 검색할 때 명령 시간 제한을 적용 하도록 수정 합니다. | 
| .NET Core (미리 보기) | 파일에 대 한 진단 로깅을 수정 합니다. | 
| .NET Core (미리 보기) | 스트림을 사용 하 여 테이블 데이터를 내보내 많은 테이블을 지원 합니다. | 
| &nbsp; | &nbsp; |

## <a name="182-sqlpackage"></a>18.2 sqlpackage

|플랫폼|다운로드|릴리스 날짜|버전 옵션|빌드
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

릴리스 날짜: &nbsp; 2018년 6월 22일  
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
| 가져오기 | Azure SQL Database .bacpac를 온-프레미스 인스턴스로 가져올 때 _이 버전의 SQL Server에서는 암호가 없는 데이터베이스 마스터 키가 지원되지 않습니다_로 인한 오류를 수정했습니다. |
| 그래프 | 그래프 테이블에 대한 확인되지 않은 의사(pseudo) 열 오류를 수정했습니다. |
| 스키마 비교 | 스키마를 비교 하는 SQL 인증을 수정 했습니다. | 
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
