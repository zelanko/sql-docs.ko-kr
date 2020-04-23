---
title: 버그 수정 목록
description: 이 페이지에는 Microsoft ODBC Driver 17 for SQL Server부터 각 릴리스에서 수정된 버그의 목록이 포함되어 있습니다.
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 0541f875230426f6ebc0fd1f90ac06110861f025
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81629723"
---
# <a name="list-of-bugs-fixed"></a>버그 수정 목록

이 페이지에는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]부터 각 릴리스에서 수정된 버그의 목록이 포함되어 있습니다.

### <a name="bug-fixes-in-the-msconame-odbc-driver-1752-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

- Alpine Linux 패키지에 msodbcsql.h 추가

### <a name="bug-fixes-in-the-msconame-odbc-driver-175-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

- Linux/macOS에서 AKV CMK 메타데이터 해시 계산 수정
- OpenSSL 1.0.0을 로드할 때 오류 수정
- ISO-8859-1 및 ISO-8859-2 코드 페이지를 사용할 때 변환 문제 해결
- macOS의 내부 라이브러리 이름을 버전 번호를 포함하도록 수정
- 별도의 길이 및 표시기 바인딩을 사용하는 경우 null 표시기의 설정 수정

### <a name="bug-fixes-in-the-msconame-odbc-driver-1742-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

 - 프로세스 ID와 애플리케이션 이름이 SQL Server에 올바르게 전송되지 않는 문제(sys.dm_exec_sessions 분석의 경우) 수정(Linux)
 - libuuid에 대한 중복 종속성 제거(Linux)
 - SQL Server 2019에 UTF8 데이터를 전송할 때의 버그 수정
 - "@euro"로 끝나는 로캘이 올바르게 검색되지 않는 버그 수정(Linux)
 - Always Encrypted를 사용하는 동안 출력 매개 변수로 페치할 때 잘못 반환되는 XML 데이터 수정

### <a name="bug-fixes-in-the-msconame-odbc-driver-174-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

- MARS(Multiple Active Results Sets)를 사용할 때의 간헐적인 중단 수정
- 비동기 알림을 사용할 때의 연결 복원력 중지 수정
- 다중 스레드 연결 시도에 대한 진단 레코드를 검색할 때의 크래시 해결
- SQL_USER_NAME 및 SQL_DATA_SOURCE_READ_ONLY를 사용하여 SQLGetInfo()를 호출한 후 다시 연결 시 '암호화가 지원되지 않음' 수정
- Azure Active Directory 대화형 인증 중 COM 초기화 오류 수정
- 멀티 바이트 UTF8 데이터의 SQLGetData() 수정
- SQLGetData()를 사용하는 sql_variant 열 길이 검색 수정
- bcp를 사용하는 7,992바이트 초과 sql_variant 열 가져오기 수정
- 반각 문자 데이터의 서버에 올바른 인코딩 전송 수정

### <a name="bug-fixes-in-the-msconame-odbc-driver-173-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

- TCP 전송 알림 이벤트 핸들 메모리 누수 수정
- msodbcsql.h 헤더 파일에서 열거형 _SQL_FILESTREAM_DESIRED_ACCESS의 재정의 문제 해결
- Linux용 msodbcsql.h 헤더 파일에서 ACCESS_TOKEN 및 AUTHENTICATION 관련 정의 누락 수정

### <a name="bug-fixes-in-the-msconame-odbc-driver-172-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

- Azure Active Directory 인증에 대한 오류 메시지 수정
- 로캘 환경 변수가 다르게 설정되었을 때의 인코딩 검색 수정
- 연결 복구를 진행하는 동안 연결이 끊어질 때의 크래시 수정
- 연결 활동성 검색 수정
- 닫힌 소켓을 잘못 검색하는 문제 해결
- 실패한 복구에서 문 핸들 해제를 시도할 때의 무한 대기 수정
- Windows에 버전 13 및 17이 함께 설치된 경우 잘못된 제거 동작 수정
- 이전 Windows 플랫폼(Windows 7, 8 및 Server 2012)에서 암호 해독 동작 수정
- Windows에서 ADAL 인증을 사용할 때의 캐시 문제 해결
- Windows에서 추적 로그를 잠그고 덮어쓰는 문제 해결

### <a name="bug-fixes-in-the-msconame-odbc-driver-171-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

- MARS가 사용하도록 설정되고 연결 특성 "Encrypt=yes"인 상태에서 SQLFreeHandle을 호출할 때의 1초 지연 수정
- SQLGetData에서 전달된 버퍼의 크기가 검색되는 데이터보다 작을 때의 오류 22003 크래시 수정(Windows)
- 잘린 ADAL 오류 메시지 수정
- 부동 소수점 숫자를 정수로 변환할 때 32비트 창에서 드물게 발생하는 버그 수정
- Always Encrypted가 켜진 상태에서 10진수 필드에 실수(double)를 삽입하면 데이터 잘림 오류가 반환되는 문제 해결
- macOS 설치 프로그램에 대한 경고 수정
- 연결 복원력과 연결 풀링이 모두 사용하도록 설정되어 세션이 서버에 의해 삭제되는 경우 세션 복구를 시도하는 동안 SQL Server로 잘못된 상태를 보내는 문제 해결

### <a name="bug-fixes-in-the-msconame-odbc-driver-17-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버그 수정

- Kerberos 인증을 사용할 때 대량 삽입이 실패하고 "액세스 거부" 오류가 발생하는 버그 수정
- 2\.3.1 이전 버전에 존재하는 unixODBC 버그에 대한 해결 방법 제거(드라이버가 unixODBC로 전달되는 특정 버퍼의 크기를 두 배로 증가시킴)
- ColumnEncryption=enabled를 사용할 때의 연결 복원력(다시 연결) 중단 수정
- "Active Directory 대화형 인증" 옵션을 사용할 때 Azure 인증 창이 응답하지 않을 수 있는 DSN 생성 버그 수정(Windows)
- 비동기 실행을 사용할 때 ODBC를 종료하는 동안 드물게 발생하는 크래시 수정(연결 핸들을 지울 때 발생)
- SQL 드라이버에서 긴 저장 프로시저를 실행하는 동안 CPU 사용량이 높은 경우 발생하는 문제 해결
- 암호화된 varbinary(max) 열의 데이터를 변환하지 않고 검색할 수 없는 문제 해결
- 정적 커서에서 SQLGetData()를 사용하여 null varchar(max) 암호화된 열을 페치한 후 다음 열이 데이터를 포함하는 경우에도 null 처리되는 문제 해결
- Always Encrypted가 켜진 상태에서 varbinary(max) 필드를 페치할 때의 문제 해결
- setlocale()이 Always Encrypted에서 작동하지 않는 문제 해결
- Always Encrypted가 켜진 상태에서 XML 형식 저장 프로시저 매개 변수에 대해 호출될 때 SQLDescribeParam()가 오류를 반환하는 문제 해결
- SQLTables에서 이스케이프된 밑줄이 작동하지 않는 문제 해결
- Linux에서 와이드 문자로 반환될 때 히브리어 데이터(varchar)가 잘리는 버그 수정
- UTF-8 애플리케이션에서 Shift-JIS로 인코딩된 char/varchar를 쿼리할 때의 문제 해결
- macOS에서 SQL_DRIVER_NAME 매개 변수를 사용하여 SQLGetInfo를 호출할 경우 Linux 스타일 파일 이름을 반환하는 버그 수정
- BCP 유틸리티를 사용하여 32kb보다 큰 입력 파일의 Windows-1252 문자 데이터를 VARCHAR 열로 로드할 때 오류가 발생하는 문제 해결
