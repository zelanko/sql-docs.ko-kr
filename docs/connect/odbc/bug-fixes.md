---
title: 수정 된 버그 목록 | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 6ef479b95e62c2f489b06905b33318a877a60ad5
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784795"
---
# <a name="list-of-bugs-fixed"></a>수정 된 버그 목록

이 페이지부터 각 릴리스에서 수정 된 버그 목록이 들어 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>버그 수정 된 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Azure Active Directory 인증에 대 한 오류 메시지를 고정
- 인코딩 감지 고정된 로캘 환경 변수를 다르게 설정 된 경우
- 충돌 시 진행에서 연결 복구를 사용 하 여 연결을 끊을 고정
- 연결 끊김 검색 문제 수정된
- 닫힌된 소켓의 잘못 된 고정된 검색
- 실패 한 복구 하는 동안 문 핸들을 해제 하려고 할 때은 무한 대기를 고정
- 버전 13 및 17 모두 Windows에 설치 되 면 잘못 된 제거 동작을 수정
- 이전 Windows 플랫폼 (Windows 7, 8 및 Server 2012)에서 고정된 암호 해독 동작
- Windows에서 ADAL 인증을 사용 하는 경우에 캐시 문제를 해결 함
- 잠금가 하는 문제를 해결 하 고 Windows에서 로그 추적을 덮어쓰기

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>버그 수정 된 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17.1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- MARS가 활성화 된 SQLFreeHandle 및 연결 특성을 호출 하는 경우 1 초 지연 고정 "Encrypt = yes"
- 전달 된 버퍼의 크기가 작은 경우 SQLGetData 검색 중인 데이터 (Windows)에 오류 22003 충돌 해결
- 잘린된 ADAL 오류 메시지를 고정합니다.
- 소수점 숫자 정수를 부동으로 변환 하는 경우 32 비트 Windows에서 드문 버그 수정
- 위치에서 상시 암호화와 함께 10 진수 필드에 이중 삽입 반환 데이터 잘림 오류 문제를 해결 함
- MacOS 설치 관리자에서 경고를 수정 했습니다.
- 연결 복원 력 및 연결 풀링 모두 설정 된 경우 서버에서 삭제할 세션을 일으키는 세션 복구를 시도 하는 동안 잘못 된 상태가 SQL Server로 보내기 고정

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>버그 수정 된 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- 버그를 수정 했습니다 대량 삽입 "액세스 거부" 오류와 함께 실패할 수 있습니다 때 Kerberos 인증을 사용 하는 경우
- 버전 2.3.1 아래에 있는 unixODBC 버그에 대 한 제거 해결 (unixODBC에 전달 된 특정 버퍼의 크기 두 배로 증가 드라이버)
- 연결 복원 력 고정 ColumnEncryption를 사용 하는 경우 중단 (다시) = 사용
- 고정 DSN 만들기 버그가 있는 경우 "Active Directory 대화형 인증"을 사용 하 여 옵션 Azure 인증 창이 될 응답 하지 않습니다 (Windows)
- 비동기 실행 (연결 핸들을 지울 때 발생) 사용 하는 경우 드문 충돌을 ODBC 종료 하는 동안 고정
- SQL 드라이버 높은 CPU 사용량 장기 저장된 프로시저를 실행 하는 동안 발생 하는 위치는 문제가 해결 되었습니다.
- 변환 하지 않고 암호화 된 varbinary (max) 열에 데이터를 검색 하는 고정 된 수
- 여기서는 null varchar (max) 한 후 암호화 된 열 인출 되는 정적 커서에 대해 SQLGetData()를 사용 하 여 한 문제를 해결, 열은 또한 null이 되어 데이터가 있는 경우에
- 항상 암호화 된 varbinary (max) 필드에서 가져오는 것과 문제를 해결 했습니다.
- 상시 암호화와 함께 작동 하지 setlocale()의 문제 해결
- 상시 암호화와 함께 XML 형식 저장 프로시저 매개 변수에서 호출 하는 동안 오류가 발생 했습니다. 반환 SQLDescribeParam()를 사용 하 여 문제를 해결 했습니다.
- 고정된 이스케이프 된 밑줄 SQLTables에서 작동 하지 않음
- Hebrew 데이터 (varchar)는 Linux의 와이드 문자를 반환 하는 경우 잘립니다 버그가 수정 되었습니다.
- Shift JIS로 인코딩된 char/varchar u t F-8 응용 프로그램에서 쿼리 문제를 해결 했습니다.
- 여기서 SQLGetInfo SQL_DRIVER_NAME 매개 변수를 사용 하 여 호출 반환 된 Linux 스타일 filename MacOS에서 버그를 수정 했습니다.
- 입력을 사용 하 여 Windows-1252 문자 데이터를 로드 파일 바이트 BCP 유틸리티를 사용 하 여 VARCHAR 열에 오류를 초래 하는 32k 보다 큰 문제를 해결 함
