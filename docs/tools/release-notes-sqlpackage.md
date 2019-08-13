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
ms.openlocfilehash: 590ca8048d45d9832ff53775512f991268843872
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809457"
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

## <a name="182-sqlpackage"></a>18.2 sqlpackage

릴리스 날짜: &nbsp; 2019년 4월 15일  
빌드: &nbsp; 15.0.4384.2 

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 에지 제약 조건 및 에지 제약 조건 절에 대한 그래프 테이블 지원을 추가합니다. | &nbsp; |
| SQL Server 2016 이상의 인덱스 키에 대해 32개 열을 지원하도록 모델 유효성 검사 규칙을 사용하도록 설정했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 사용 중인 지원되지 않은 쿼리 힌트로 인한 SQL Server 2016 RTM 데이터베이스 리버스 엔지니어링을 수정합니다. | &nbsp; |
| create filegroup 문을 만들기 전에 발생하도록 auto close alter 문의 배포 순서를 수정합니다. | &nbsp; |
| 'URL' 문자열이 최상위 토큰으로 해석된 ScriptDom 구문 분석 회귀를 수정합니다. | &nbsp; |
| alter table add index 문을 구문 분석할 때 null 참조 예외를 수정합니다. | &nbsp; |
| 항상 다른 것으로 표시되는 nullable 지속형 계산 열의 스키마 비교를 수정했습니다.| &nbsp; |
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>18.1 sqlpackage

릴리스 날짜: &nbsp; 2019년 2월 1일  
빌드: &nbsp; 15.0.4316.1  
미리 보기 릴리스입니다.

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| UTF8 데이터 정렬에 대한 지원을 추가했습니다. | &nbsp; |
| 인덱싱된 뷰에서 비클러스터형 columnstore 인덱스를 사용하도록 설정했습니다. | &nbsp; |
| .NET Core 2.2로 이동했습니다. | &nbsp; |
| .NET Core에서 스키마 비교에 메모리 기반 스토리지를 사용합니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 리버스 엔지니어링 쿼리에 레거시 카디널리티 평가기를 사용하기 위한 성능 수정입니다. | &nbsp; |
| 스크립트를 생성할 때 중요한 스키마 비교 성능 문제를 수정했습니다. | &nbsp; |
| 특정 확장 이벤트(xevent) 세션을 무시하도록 스키마 드리프트 검색 논리를 수정했습니다. | &nbsp; |
| 그래프 테이블의 가져오기 순서를 수정했습니다. | &nbsp; |
| 개체 권한과 함께 외부 테이블 내보내기를 수정했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

이 릴리스에는 .NET Core 2.2를 대상으로 하는 sqlpackage의 플랫폼 간 미리 보기 빌드가 포함됩니다. sqlpackage는 macOS 및 Linux에서 실행할 수 있습니다.

| 알려진 문제 | 세부 정보 |
| :---------- | :------ |
| 빌드 및 배포 참가자가 지원되지 않습니다. | &nbsp; |
| Json 데이터 serialization을 사용하는 이전 .dacpac 및.bacpac 파일이 지원되지 않습니다. | &nbsp; |
| 대/소문자 구분 파일 시스템 문제로 인해 참조된.dacpacs(예: master.dacpac)를 확인할 수 없습니다. | 이 문제를 해결하려면 참조 파일의 이름을 대문자로 바꿉니다(예: MASTER.BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

릴리스 날짜: &nbsp; 2018년 10월 24일  
빌드: &nbsp; 15.0.4200.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 데이터베이스 호환성 수준 150에 대한 지원을 추가했습니다. | &nbsp; |
| Managed Instance에 대한 지원을 추가했습니다. | &nbsp; |
| 데이터베이스 작업의 병렬 처리 수준을 지정하는 MaxParallelism 명령줄 매개 변수를 추가했습니다. | &nbsp; |
| SQL Server에 연결할 때 인증 토큰을 지정하는 AccessToken 명령줄 매개 변수를 추가했습니다. | &nbsp; |
| 가져오기에 대한 BLOB/CLOB 데이터 형식을 스트리밍하도록 지원을 추가했습니다. | &nbsp; |
| 스칼라 UDF 'INLINE' 옵션에 대한 지원을 추가했습니다. | &nbsp; |
| 그래프 테이블의 'MERGE' 구문에 대한 지원을 추가했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 그래프 테이블에 대한 확인되지 않은 의사(pseudo) 열을 수정했습니다. | &nbsp; |
| 메모리 최적화 테이블이 사용되는 경우 메모리 최적화 파일 그룹이 포함된 데이터베이스 만들기를 수정했습니다. | &nbsp; |
| 외부 테이블에 확장 속성 포함을 수정했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

릴리스 날짜: &nbsp; 2018년 6월 22일  
빌드: &nbsp; 14.0.4079.2

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| SqlClient 예외 메시지를 포함하여 연결 실패의 오류 메시지를 향상했습니다. | &nbsp; |
| 가져오기/내보내기를 위해 단일 파티션 인덱스에서 인덱스 압축을 지원합니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| SQL 2017 이상에서 XML 열 집합의 리버스 엔지니어링 문제를 수정했습니다. | &nbsp; |
| Azure SQL Database에서 데이터베이스 호환성 수준 140 스크립팅이 무시된 문제를 수정했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

릴리스 날짜: &nbsp; 2018년 1월 25일  
빌드: &nbsp; 14.0.3917.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 많은 수의 중첩 문이 있는 Transact-SQL을 구문 분석하는 ThreadMaxStackSize 명령줄 매개 변수를 추가했습니다. | &nbsp; |
| 데이터베이스 카탈로그 데이터 정렬 지원입니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| Azure SQL Database .bacpac를 온-프레미스 인스턴스로 가져올 때 ‘이 버전의 SQL Server에서는 암호가 없는 데이터베이스 마스터 키 지원되지 않습니다’로 인한 오류를 수정했습니다.  | &nbsp; |
| 그래프 테이블에 대한 확인되지 않은 의사(pseudo) 열 오류를 수정했습니다. | &nbsp; |
| 스키마를 비교하기 위해 SQL 인증과 함께 SchemaCompareDataModel 사용을 수정했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

릴리스 날짜: &nbsp; 2017년 12월 12일  
빌드: &nbsp; 14.0.3881.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| SQL 2017 이상 및 Azure SQL Database에서 ‘임시 보존 정책’에 대한 지원을  추가했습니다. | &nbsp; |
| 진단 정보를 저장할 파일 경로를 지정하는 /DiagnosticsFile:"C:\Temp\sqlpackage.log" 명령줄 매개 변수를 추가했습니다. | &nbsp; |
| 진단 정보를 콘솔에 기록하는 /Diagnostics 명령줄 매개 변수를 추가했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 인식할 수 없는 데이터베이스 호환성 수준이 발생하는 경우 차단하지 않습니다. | 대신 최신 Azure SQL Database 또는 온-프레미스 플랫폼이 간주됩니다. |
| &nbsp; | &nbsp; |
