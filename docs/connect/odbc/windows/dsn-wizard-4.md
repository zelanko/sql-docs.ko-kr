---
title: 데이터 원본 마법사 화면 4 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c8a5a785f7c208d8543f9ec3a27d34b34f7a918
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724371"
---
# <a name="data-source-wizard-screen-4"></a>데이터 원본 마법사 화면 4

SQL Server 메시지에 사용할 언어, 문자 집합 변환 및 ODBC Driver for SQL Server가 국가별 설정을 사용해야 하는지 여부를 지정합니다. 또한 장시간 실행되는 쿼리와 드라이버 통계 설정에 대한 로깅을 제어할 수도 있습니다.

## <a name="options"></a>Options

### <a name="change-the-language-of-sql-server-system-messages-to"></a>SQL Server 시스템 메시지 언어를 다음으로 변경

각 SQL Server의 인스턴스는 집합별로 다른 언어(예: 영어, 스페인어, 프랑스어 등)로 된 여러 시스템 메시지 집합을 가질 수 있습니다. 데이터 원본이 여러 시스템 메시지 집합이 있는 서버에 대해 정의된 경우 시스템 메시지에 사용할 언어를 지정할 수 있습니다. 목록에서 언어를 클릭합니다. 이 옵션은 SQL Server에 하나의 언어만 설치된 경우에 사용할 수 없습니다.

### <a name="use-strong-encryption-for-data"></a>데이터에 대하여 강력한 암호화 사용

이 옵션을 선택하면 DSN을 사용하여 설정된 연결을 통해 전달되는 데이터가 암호화됩니다. 이 확인란의 선택을 취소하는 경우에도 로그인은 기본적으로 암호화됩니다.

### <a name="trust-server-certificate"></a>서버 인증서 신뢰

이 옵션은 경우에만 적용 **강력한 암호화를 사용 하 여 데이터에 대 한** 사용 가능 합니다. 옵션을 선택 하면 서버의 올바른 호스트 이름이 있고 신뢰할 수 있는 인증 기관에서 발급 하는 서버의 인증서 검사 하지 않습니다. 

### <a name="perform-translation-for-character-data"></a>문자 데이터에 대한 변환 실행

이 확인란을 선택하면 ODBC Driver for SQL Server는 유니코드를 사용하여 클라이언트 컴퓨터와 SQL Server 사이에 전송된 ANSI 문자열을 변환합니다. ODBC 드라이버는 경우에 따라 클라이언트 컴퓨터에서 SQL Server 코드 페이지와 유니코드 간을 변환합니다. 이를 위해서는 SQL Server에 사용되는 코드 페이지가 클라이언트 컴퓨터에서 사용할 수 있는 코드 페이지 중 하나여야 합니다.

이 확인란을 선택하지 않으면 ANSI 문자열의 확장 문자는 클라이언트 응용 프로그램과 서버 사이에서 전송될 때 변환되지 않습니다. 클라이언트 컴퓨터가 SQL Server 코드 페이지와 다른 ACP(ANSI 코드 페이지)를 사용하는 경우 ANSI 문자열의 확장 문자가 잘못 해석될 수 있습니다. 클라이언트 컴퓨터가 SQL Server에서 사용 중인 ACP에서 동일한 코드 페이지를 사용하는 경우 확장 문자는 올바르게 해석됩니다.

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>통화, 숫자, 날짜 및 시간 표기에 국가별 설정 사용

드라이버가 문자 출력 문자열의 통화, 숫자, 날짜 및 시간에 서식을 지정할 때 클라이언트 컴퓨터의 국가별 설정을 사용하도록 지정합니다. 드라이버는 데이터 원본을 통해 연결된 사용자의 Windows 로그인 계정에 대한 기본 국가별 설정을 사용합니다. 데이터를 처리하지 않고 단순히 표시하기만 하는 응용 프로그램에 대해 이 옵션을 선택하십시오.

### <a name="save-long-running-queries-to-the-log-file"></a>장기 실행 쿼리를 다음 로그 파일에 저장

드라이버가 **장기 쿼리 시간** 값보다 오래 걸리는 모든 쿼리를 기록하도록 지정합니다. 장기 실행 쿼리는 지정된 파일에 기록됩니다. 로그 파일을 지정하려면 상자에 전체 경로와 파일 이름을 입력하거나 기존 파일 디렉터리를 통해 탐색하여 로그 파일을 선택하도록 **찾아보기**를 클릭합니다.

### <a name="long-query-time-milliseconds"></a>장기 쿼리 시간(밀리초)

장기 실행 쿼리 기록을 위한 임계값을 밀리초 단위로 지정합니다. 지정된 시간(밀리초)보다 오랫동안 실행되는 모든 쿼리가 기록됩니다.

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>ODBC 드라이버 통계를 다음 로그 파일에 기록

통계를 기록하도록 지정합니다. 통계는 지정된 파일에 기록됩니다. 로그 파일을 지정하려면 상자에 전체 경로와 파일 이름을 입력하거나 기존 파일 디렉터리를 통해 탐색하여 로그 파일을 선택하도록 **찾아보기**를 클릭합니다.

통계 로그는 탭으로 구분된 파일이며, Microsoft Excel 또는 탭으로 구분된 파일을 지원하는 기타 응용 프로그램으로 분석할 수 있습니다.

### <a name="connect-retry-count"></a>연결 다시 시도 횟수

실패 한 연결 시도 다시 시도 횟수를 지정 합니다.

### <a name="connect-retry-interval-seconds"></a>연결 다시 시도 간격(초)

각 연결 다시 시도 간격 (초) 수를 지정합니다. 이 작업에 대 한 자세한 내용은 및 **연결 다시 시도 횟수가** 옵션을 참조 하세요 [Connection Resiliency in Windows ODBC 드라이버](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)합니다.

### <a name="back"></a>뒤로

마법사의 이전 페이지로 다시 이동 하려면이 단추를 클릭 합니다.

### <a name="finish"></a>마침

이 화면에 지정 된 정보를 완료 하는 경우 클릭할 수 있습니다 **완료**합니다. DSN이 및 마법사의 다른 화면에 지정 된 모든 특성을 사용 하 여 만들어지고 새로 만든 DSN을 테스트할 수 있는 기회를 제공 됩니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 3](../../../connect/odbc/windows/dsn-wizard-3.md)
