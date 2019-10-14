---
title: 수정 된 버그 목록 | Microsoft Docs
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
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 2b939db6ac0f89075b39ba74eadb0e86e63e3980
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041218"
---
# <a name="list-of-bugs-fixed"></a>수정 된 버그 목록

이 페이지에는 각 릴리스에서 수정 된 버그 목록이 포함 되어 있습니다 .이 목록에는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]부터 시작 됩니다.

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-1742-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC Driver 17.4.2의 버그 수정

 - 프로세스 ID 및 응용 프로그램 이름이 SQL Server (_exec_sessions 분석의 경우)에 올바르게 전송 되지 않는 문제를 해결 합니다 (Linux).
 - Li, uid (Linux)에 대 한 중복 종속성을 제거 했습니다.
 - SQL Server 2019에 UTF8 데이터를 전송 하는 버그를 수정 합니다.
 - "@euro"으로 끝나는 로캘이 올바르게 검색 되지 않는 버그 수정 (Linux)
 - Always Encrypted를 사용 하는 동안 output 매개 변수로 인출할 때 잘못 반환 되는 XML 데이터에 대 한 수정

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-174-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] 의 버그 수정-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 ODBC 드라이버 17.4-1

- MARS (Multiple Active Results Sets)를 사용 하는 경우 간헐적인 중단에 대 한 수정
- 비동기 알림을 사용 하는 경우 연결 복원 력 수정 중지
- 다중 스레드 연결 시도에 대 한 진단 레코드를 검색할 때 충돌 해결
- SQL_USER_NAME 및 SQL_DATA_SOURCE_READ_ONLY를 사용 하 여 SQLGetInfo ()를 호출한 후 다시 연결할 때 ' 암호화가 지원 되지 않음 ' 수정
- Azure Active Directory 대화형 인증을 수행 하는 동안 COM 초기화 오류 수정
- 멀티 바이트 UTF8 데이터의 SQLGetData () 수정
- SQLGetData ()를 사용 하 여 sql_variant 열의 길이 검색 수정
- Bcp를 사용 하 여 7992 바이트를 초과 하는 sql_variant 열 가져오기 수정
- 좁은 문자 데이터의 서버에 올바른 인코딩 전송 수정

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] 의 버그 수정-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 ODBC 드라이버 17.3-1

- TCP 송신 알림 이벤트 핸들 메모리 누수가 해결 됨
- Msodbcsql .h 헤더 파일에서 enum _SQL_FILESTREAM_DESIRED_ACCESS의 재정의 문제를 수정 했습니다.
- Linux 용 msodbcsql .h 헤더 파일에 누락 된 ACCESS_TOKEN 및 인증 관련 정의가 수정 되었습니다.

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] 의 버그 수정-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 ODBC 드라이버 17.2-1

- Azure Active Directory 인증에 대 한 오류 메시지 수정 됨
- 로캘 환경 변수가 다르게 설정 된 경우 인코딩 검색 고정
- 연결 복구를 진행 하는 동안 연결이 끊어질 때 충돌 해결 됨
- Connection 선거의의 검색 문제를 수정 했습니다.
- 닫힌 소켓의 잘못 된 검색 문제 해결
- 복구에 실패 하는 동안 문 핸들을 해제 하려고 할 때 무한 대기를 수정 했습니다.
- Windows에 버전 13 및 17이 둘 다 설치 된 경우 잘못 된 제거 동작을 수정 함
- 이전 Windows 플랫폼에서 암호 해독 동작 수정 (Windows 7, 8 및 Server 2012)
- Windows에서 ADAL 인증을 사용 하는 경우 캐시 문제 해결
- Windows에서 추적 로그를 잠그고 덮어쓰는 문제를 해결 했습니다.

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] 의 버그 수정-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 ODBC 드라이버 17.1-1

- MARS를 사용 하는 SQLFreeHandle 및 연결 특성 "Encrypt = yes"를 호출할 때 1 초 지연 수정
- 전달 된 버퍼의 크기가 더 작은 경우 SQLGetData에서 오류 22003 충돌 해결 됨 (Windows)
- 잘린 ADAL 오류 메시지 수정 됨
- 부동 소수점 숫자를 정수로 변환할 때 32 비트 창에서 드물게 발생 하는 버그를 수정 했습니다.
- Always Encrypted의 decimal 필드에 double을 삽입 하면 데이터 잘림 오류가 반환 되는 문제가 해결 됨
- MacOS 설치 관리자에 대 한 경고 해결
- 연결 복원 및 연결 풀링이 모두 사용 하도록 설정 되어 세션이 서버에 의해 삭제 되는 경우 세션 복구를 시도 하는 동안 SQL Server로 잘못 된 상태 보내기가 수정 되었습니다.

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] 의 버그 수정-0 용 ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Kerberos 인증을 사용할 때 대량 삽입이 실패 하 고 "액세스 거부" 오류가 발생 하는 버그가 수정 되었습니다.
- 2\.3.1 아래 버전에서 제공 되는 총 Xodbc 버그에 대 한 해결 방법이 제거 되었습니다 (드라이버는 총 Xodbc로 전달 되는 특정 버퍼의 크기를 두 배로 증가).
- ColumnEncryption을 사용 하는 경우 연결 복원 력 (다시 연결)이 지연 됨 = 사용
- "Active Directory 대화형 인증" 옵션을 사용 하는 경우 Azure 인증 창이 응답 하지 않을 수 있는 DSN 생성 버그를 수정 했습니다 (Windows).
- 비동기 실행을 사용 하는 경우 (연결 핸들을 지울 때 발생) ODBC를 종료 하는 동안 드물게 발생 하는 충돌 문제 해결
- SQL 드라이버에서 긴 저장 프로시저를 실행 하는 동안 CPU 사용량이 높은 경우 발생 하는 문제를 해결 함
- 변환 하지 않고 암호화 된 varbinary (max) 열의 데이터를 검색할 수 없는 문제 해결
- 정적 커서에서 SQLGetData ()를 사용 하 여 null varchar (max) 암호화 된 열이 인출 된 후에도 다음 열이 데이터를 포함 하는 경우에도 nulled 되는 문제를 해결 함
- Always Encrypted에서 varbinary (max) 필드를 가져오는 문제를 수정 했습니다.
- Always Encrypted에서 사용 하지 않는 setlocale ()의 문제를 수정 했습니다.
- Always Encrypted on으로 설정 된 XML 형식 저장 프로시저 매개 변수에 대해 호출 될 때 SQLDescribeParam ()에서 오류를 반환 하는 문제가 해결 되었습니다.
- SQLTables에서 작동 하지 않는 이스케이프 된 밑줄 수정
- Linux에서 와이드 문자로 반환 될 때 히브리어 데이터 (varchar)가 잘리는 버그 수정
- UTF-8 응용 프로그램에서 shift-jis로 인코딩된 char/varchar를 쿼리 하는 문제를 해결 함
- SQL_DRIVER_NAME 매개 변수를 사용 하 여 SQLGetInfo를 호출 하 여 MacOS에서 Linux 스타일 파일 이름을 반환 하는 버그를 수정 했습니다.
- BCP 유틸리티를 사용 하 여 32k 바이트 보다 큰 입력 파일을 VARCHAR 열로 사용 하 여 Windows-1252 문자 데이터를 로드할 때 오류가 발생 하는 문제를 해결 함
