---
title: Microsoft DacFx & sqlpackage 릴리스 정보 | Microsoft Docs
description: Microsoft sqlpackage 릴리스 정보
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 69b3b5c9574578b286b882b7d2125b0bb984759b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52413752"
---
# <a name="sqlpackage-release-notes"></a>sqlpackage 릴리스 정보

**[최신 버전 다운로드](sqlpackage-download.md)**

## <a name="sqlpackage-180"></a>sqlpackage 18.0

릴리스 날짜: 2018 년 10 월 24 일  
빌드: 15.0.4200.1 

릴리스는 다음 기능 및 수정 합니다.

- 데이터베이스 호환성 수준이 150에 대 한 지원이 추가 되었습니다.
- 관리 되는 인스턴스에 대 한 지원이 추가 되었습니다.
- 추가 MaxParallelism 명령줄 매개 변수를 데이터베이스 작업에 대 한 병렬 처리 수준을 지정 합니다.
- SQL Server에 연결할 때 인증 토큰을 지정 하려면 AccessToken 명령줄 매개 변수를 추가 합니다.
- 가져오기에 대 한 스트림 BLOB/CLOB 데이터 형식에 대 한 지원이 추가 되었습니다.
- 스칼라 UDF에 대 한 지원이 추가 되었습니다 'INLINE' 옵션입니다.
- 그래프 테이블의 '병합' 구문에 대 한 지원이 추가 되었습니다.
- 그래프 테이블에 대 한 고정된 확인 되지 않은 의사 (pseudo) 열입니다.
- 메모리 최적화 테이블에는 그룹을 사용 하는 메모리 최적화 된 파일을 사용 하 여 데이터베이스 만들기를 고정 합니다.
- 외부 테이블에 확장된 속성을 포함 하 여 수정 했습니다.

## <a name="sqlpackage-178"></a>sqlpackage 17.8

릴리스 날짜: 2018년 6월 22일  
빌드: 14.0.4079.2  

다음 수정 사항을 포함 하는 릴리스:

- 향상 된 SqlClient 예외 메시지를 포함 하 여 연결 실패에 대 한 오류 메시지입니다.
- Import/export에 단일 파티션 인덱스의 index 압축을 지원 합니다.
- XML 열 집합 SQL 2017 이상에 대 한 리버스 엔지니어링 문제가 수정 되었습니다.
- 문제를 해결 하 고 Azure SQL Database에 대 한 데이터베이스 호환성 수준 140을 스크립팅 무시 된 키를 누릅니다.

## <a name="sqlpackage-1741"></a>sqlpackage 17.4.1

릴리스 날짜: 2018 년 1 월 25 일  
빌드: 14.0.3917.1

다음 수정 사항을 포함 하는 릴리스:

- 온-프레미스 인스턴스를 Azure SQL Database.bacpac를 가져올 때 '암호 없이 데이터베이스 마스터 키는이 버전의 SQL Server에는 지원 되지 않습니다'으로 인해 오류를 해결 했습니다.
- 데이터베이스 카탈로그 데이터 정렬 지원 합니다.
- 그래프 테이블에 대 한 확인 되지 않은 의사 열 오류를 수정 했습니다.
- 추가 ThreadMaxStackSize 명령줄 매개 변수를 많은 수의 중첩 된 문 TSQL 구문 분석 합니다.
- SQL 인증을 사용 하 여는 SchemaCompareDataModel를 사용 하 여 스키마를 비교 하려면 고정 합니다.

## <a name="sqlpackage-1740"></a>sqlpackage 17.4.0

릴리스 날짜: 2017년 12월 12일  
빌드: 14.0.3881.1

다음 수정 사항을 포함 하는 릴리스:

- 데이터베이스 호환성 수준이 없습니다 발생 이해 하는 경우 차단 하지 않습니다. 대신 최신 Azure SQL Database 또는 온-프레미스 플랫폼으로 간주 됩니다.
- '임시 재방문 주기 정책' SQL2017 + 및 Azure SQL Database에 대 한 지원이 추가 되었습니다.
- /DiagnosticsFile:"C:\Temp\sqlpackage.log 추가" 명령줄 매개 변수 진단 정보를 저장할 파일 경로 지정 합니다.
- 추가 /Diagnostics 명령줄 매개 변수를 콘솔에 진단 정보를 기록 합니다.

## <a name="sqlpackage-on-macos-and-linux-net-core-preview"></a>macOS 및 Linux.NET Core (미리 보기)에서 sqlpackage

릴리스 날짜: 2018년 11월 15일  
빌드: 15.0.4240.1

이 릴리스에서.NET Core 2.1을 대상으로 하는 sqlpackage의 플랫폼 간 미리 보기 빌드를 포함 및 macOS 및 Linux에서 실행할 수 있습니다. 

다음 수정 사항을 포함 하는 릴리스:

- .NET Core 2.1로 이동 
- SQL CLR UDT 형식을 비롯 한 CLR UDT 형식에 대 한 지원: SqlGeography, SqlGeometry, 및 SqlHierarchyId 합니다.

이 릴리스는 다음과 같은 알려진된 문제가 사용 하 여 초기 미리 보기:

- /P:CommandTimeout 매개 변수를 120 코딩 하드 되어 있습니다.
- 빌드 및 배포 참가자가 지원 되지 않습니다.
- Json 데이터 serialization을 사용 하는 오래 된.dacpac 및.bacpac 파일 지원 되지 않습니다.
- 참조 된.dacpacs (예를 들어 master.dacpac) 대/소문자 구분 파일 시스템 문제로 인해 확인할 수 없습니다.
  - 참조 파일 (예를 들어 마스터 모두 대문자로 변경 하려면이 문제를 해결입니다. BACPAC)로 설정 합니다.
