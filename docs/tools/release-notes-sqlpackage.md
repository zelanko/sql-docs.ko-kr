---
title: SqlPackage 및 DacFx에 대 한 릴리스 정보 | Microsoft Docs
description: Microsoft sqlpackage에 대 한 릴리스 정보입니다.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: de45add2b02686f990d68f7c1c23eec385848751
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538779"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe에 대 한 릴리스 정보

**[최신 버전 다운로드](sqlpackage-download.md)**

이 문서는 기능 및 수정 SqlPackage.exe의 릴리스 버전을 전달한 나열 합니다.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="181-sqlpackage"></a>18.1 sqlpackage

릴리스 날짜: &nbsp; 2019년 2월 1일  
빌드: &nbsp; 15.0.4316.1  
미리 보기 릴리스입니다.

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| UTF8 데이터 정렬에 대 한 지원이 추가 되었습니다. | &nbsp; |
| 인덱싱된 뷰의 비클러스터형 columnstore 인덱스를 사용할 수 있습니다. | &nbsp; |
| .NET Core 2.2로 이동 합니다. | &nbsp; |
| .NET Core에서 스키마 비교에 대 한 지원 되는 메모리 내 저장소를 사용 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 성능 리버스 엔지니어링 쿼리에 대 한 레거시 카디널리티 평가기를 사용 하도록 수정 합니다. | &nbsp; |
| 스크립트를 생성 하는 경우 중요 한 스키마 비교 성능 문제가 수정 되었습니다. | &nbsp; |
| 특정 확장된 이벤트 (xevent) 세션을 무시 하도록 스키마 드리프트 검색 논리를 수정 했습니다. | &nbsp; |
| 고정된 가져오기 그래프 테이블에 대 한 순서입니다. | &nbsp; |
| 외부 테이블 개체 사용 권한과 함께 내보낼 수정 되었습니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

이 릴리스에서.NET Core 2.2를 대상으로 하는 sqlpackage의 플랫폼 간 미리 보기 빌드를 포함 합니다. Sqlpackage는 macOS 및 Linux에서 실행할 수 있습니다.

| 알려진 문제 | 세부 정보 |
| :---------- | :------ |
| 빌드 및 배포 참가자가 지원 되지 않습니다. | &nbsp; |
| Json 데이터 serialization을 사용 하는 오래 된.dacpac 및.bacpac 파일 지원 되지 않습니다. | &nbsp; |
| 참조 된.dacpacs (예를 들어 master.dacpac) 대/소문자 구분 파일 시스템 문제로 인해 확인할 수 없습니다. | 참조 파일 (예를 들어 마스터 모두 대문자로 변경 하려면이 문제를 해결입니다. BACPAC)로 설정 합니다. |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

릴리스 날짜: &nbsp; 2018 년 10 월 24 일  
빌드: &nbsp; 15.0.4200.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 데이터베이스 호환성 수준이 150에 대 한 지원이 추가 되었습니다. | &nbsp; |
| 관리 되는 인스턴스에 대 한 지원이 추가 되었습니다. | &nbsp; |
| 추가 MaxParallelism 명령줄 매개 변수를 데이터베이스 작업에 대 한 병렬 처리 수준을 지정 합니다. | &nbsp; |
| 추가 AccessToken 명령줄 매개 변수를 SQL Server에 연결할 때 인증 토큰을 지정 합니다. | &nbsp; |
| 가져오기에 대 한 스트림 BLOB/CLOB 데이터 형식에 대 한 지원이 추가 되었습니다. | &nbsp; |
| 스칼라 UDF에 대 한 지원이 추가 되었습니다 'INLINE' 옵션입니다. | &nbsp; |
| 그래프 테이블의 '병합' 구문에 대 한 지원이 추가 되었습니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 그래프 테이블에 대 한 고정된 확인 되지 않은 의사 (pseudo) 열입니다. | &nbsp; |
| 메모리 최적화 테이블에는 그룹을 사용 하는 메모리 최적화 된 파일을 사용 하 여 데이터베이스 만들기를 고정 합니다. | &nbsp; |
| 외부 테이블에 확장된 속성을 포함 하 여 수정 했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

릴리스 날짜: &nbsp; 2018년 6월 22일  
빌드: &nbsp; 14.0.4079.2

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 향상 된 SqlClient 예외 메시지를 포함 하 여 연결 실패에 대 한 오류 메시지입니다. | &nbsp; |
| Import/export에 단일 파티션 인덱스의 index 압축을 지원 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| XML 열 집합 SQL 2017 이상에 대 한 리버스 엔지니어링 문제가 수정 되었습니다. | &nbsp; |
| 문제를 해결 하 고 Azure SQL Database에 대 한 데이터베이스 호환성 수준 140을 스크립팅 무시 된 키를 누릅니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

릴리스 날짜: &nbsp; 2018 년 1 월 25 일  
빌드: &nbsp; 14.0.3917.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 추가 ThreadMaxStackSize 명령줄 매개 변수를 중첩 된 문 수가 많은 TRANSACT-SQL 구문 분석 합니다. | &nbsp; |
| 데이터베이스 카탈로그 데이터 정렬 지원 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 온-프레미스 인스턴스를 Azure SQL Database.bacpac를 가져올 때로 인해 오류를 수정한 _암호 없이 데이터베이스 마스터 키는이 버전의 SQL Server에서 지원 되지 않습니다_합니다. | &nbsp; |
| 그래프 테이블에 대 한 확인 되지 않은 의사 열 오류를 수정 했습니다. | &nbsp; |
| SQL 인증을 사용 하 여는 SchemaCompareDataModel를 사용 하 여 스키마를 비교 하려면 고정 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

릴리스 날짜: &nbsp; 2017년 12월 12일  
빌드: &nbsp; 14.0.3881.1

### <a name="features"></a>기능

| 기능 | 세부 정보 |
| :------ | :------ |
| 에 대 한 지원이 추가 되었습니다 _임시 재방문 주기 정책을_ SQL 2017 + 및 Azure SQL Database에 있습니다. | &nbsp; |
| /DiagnosticsFile:"C:\Temp\sqlpackage.log 추가" 명령줄 매개 변수 진단 정보를 저장할 파일 경로 지정 합니다. | &nbsp; |
| 추가 /Diagnostics 명령줄 매개 변수를 콘솔에 진단 정보를 기록 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>수정 프로그램

| Fix | 세부 정보 |
| :-- | :------ |
| 인식할 수 없는 데이터베이스 호환성 수준이 발생 하는 경우 차단 하지 않습니다. | 대신 최신 Azure SQL Database 또는 온-프레미스 플랫폼으로 간주 됩니다. |
| &nbsp; | &nbsp; |
