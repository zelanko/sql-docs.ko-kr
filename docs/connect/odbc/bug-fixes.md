---
title: 수정 된 버그의 목록 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: genemi
manager: kenvh
ms.workload: Active
ms.openlocfilehash: 58da69ed6c4b7b046f8d1bc1ddf4e23b71b99a29
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="list-of-bugs-fixed"></a>수정 된 버그의 목록

이 페이지에서는 부터는 각 릴리스에서 수정 된 버그 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>버그 수정에는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17.1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 1 초 지연 MARS가 활성화 된 SQLFreeHandle 및 연결 특성을 호출할 때 고정 "Encrypt = yes"
- 고정 못한 오류 22003 중단 SQLGetData에 전달 된 버퍼 크기가 작으면 한 후 검색 중인 데이터 (Windows)
- 잘린된 ADAL 오류 메시지를 고정합니다.
- 소수점 수는 정수를 부동으로 변환 하는 경우 32 비트 Windows에서 드문 버그가 수정
- 10 진수 필드에서 상시 암호화에 이중 삽입가 반환 하는 위치 데이터 잘림 오류 문제 해결
- MacOS 설치 관리자에서 경고 수정
- 연결 복원 력 및 연결 풀링을 모두 설정 되 면 서버에서 삭제할 세션을 일으키는 세션 복구를 시도 하는 동안 잘못 된 상태가 SQL Server로 보내기 고정

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>버그 수정에는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- 버그를 수정 합니다. 대량 삽입 "액세스 거부" 오류와 함께 실패할 수 있습니다 때 Kerberos 인증을 사용 하는 경우
- 버전 2.3.1 아래에 있는 unixODBC 버그에 대 한 제거 해결 (드라이버 unixODBC에 전달 된 특정 버퍼의 크기를 두 배로 사용)
- 연결 복원 력 고정 ColumnEncryption를 사용 하는 경우 중단 (다시) = 사용
- 여기서 때 사용 하 여 "Active Directory 대화형 인증" 옵션 Azure 인증 DSN 만들기 버그 고정 창이 될 수 있습니다 응답 하지 않는 (Windows)
- 비동기 실행 (연결 핸들을 지울 때 발생) 사용 하는 ODBC 종료 하는 동안 충돌이 발생 한 드문 고정
- 문제가 해결 되었습니다. SQL 드라이버 장기 저장된 프로시저를 실행 하는 동안 CPU 사용률이 높을 발생 하는 위치
- 변환 하지 않고 암호화 된 varbinary (max) 열의 데이터를 검색할 수 고정된 없음
- 여기서 null varchar (max) 후 암호화 된 열은 사용 하 여 인출할 SQLGetData()는 정적 커서에 대해 한 문제를 해결, 다음과 같은 열은도 null이 되어 데이터가 있는 경우에
- 항상 암호화 된 varbinary (max) 필드에서 페치 관련 문제 해결
- 상시 암호화와 함께 작동 하지 setlocale()의 문제 해결
- 상시 암호화와 함께 XML 형식 저장 프로시저 매개 변수에서 호출 하는 동안 오류가 발생 했습니다. 반환 된 SQLDescribeParam() 관련 문제 해결
- SQLTables에서 작동 하지 않이 고정된 이스케이프 된 밑줄
- Linux의 와이드 문자도 반환 하는 경우 (varchar) 히브리어 데이터가 잘립니다 여기서는 버그를 수정
- Shift JIS 인코딩된 char/varchar u t F-8 응용 프로그램에서 쿼리 하는 관련 문제 해결
- 여기서 SQLGetInfo SQL_DRIVER_NAME 매개 변수와 함께 호출에서 반환 된 Linux 스타일 filename MacOS 버그 수정
- 입력을 사용 하 여 windows-1252 문자 데이터를 로드 파일 바이트 BCP 유틸리티를 사용 하 여 VARCHAR 열에 오류를 초래 32k 보다 큰 문제 해결
