---
title: 데이터 원본 마법사 화면 4 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f53180976b3a4778f687ef8a83d9438ea858c05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32855898"
---
# <a name="data-source-wizard-screen-4"></a>데이터 원본 마법사 화면 4

SQL Server 메시지에 사용할 언어를 지정, 문자 집합 변환 및 SQL Server에 대 한 ODBC 드라이버가 국가별 설정을 사용 해야 하는지 여부입니다. 또한 장시간 실행되는 쿼리와 드라이버 통계 설정에 대한 로깅을 제어할 수도 있습니다.

## <a name="options"></a>옵션

### <a name="change-the-language-of-sql-server-system-messages-to"></a>SQL Server 시스템 메시지 언어를 다음으로 변경

SQL Server의 각 인스턴스는 집합 별로 다른 언어 (예를 들어 영어, 스페인어, 프랑스어, 및 등)로 시스템 메시지의 여러 집합을 가질 수 있습니다. 데이터 원본이 여러 시스템 메시지 집합이 있는 서버에 대해 정의된 경우 시스템 메시지에 사용할 언어를 지정할 수 있습니다. 목록에서 언어를 클릭합니다. 하나만 한 언어는 SQL Server에 설치 된 경우에이 옵션을 사용할 수 없습니다.

### <a name="use-strong-encryption-for-data"></a>데이터에 대하여 강력한 암호화 사용

이 옵션을 선택하면 DSN을 사용하여 설정된 연결을 통해 전달되는 데이터가 암호화됩니다. 이 확인란의 선택을 취소하는 경우에도 로그인은 기본적으로 암호화됩니다.

### <a name="trust-server-certificate"></a>서버 인증서 신뢰

이 옵션은 경우에만 적용 **강력한 암호화를 사용 하 여 데이터에 대 한** 를 사용할 수 있습니다. 옵션을 선택 하면 서버 인증서의 신뢰할 수 있는 인증 기관에서 발급 될를 서버의 올바른 호스트 이름을 포함 하도록 검사 하지 않습니다. 

### <a name="perform-translation-for-character-data"></a>문자 데이터에 대한 변환 실행

이 확인란을 선택 하면 SQL Server 용 ODBC 드라이버는 유니코드를 사용 하 여 클라이언트 컴퓨터와 SQL Server 사이 전송 된 ANSI 문자열을 변환 합니다. ODBC 드라이버는 경우에 따라 클라이언트 컴퓨터에서 SQL Server 코드 페이지와 유니코드 간의 변환합니다. 그러기 위해서는 SQL Server에서 사용 되는 코드 페이지 클라이언트 컴퓨터에서 사용할 수 있는 코드 페이지 중 하나 여야 합니다.

이 확인란을 선택하지 않으면 ANSI 문자열의 확장 문자는 클라이언트 응용 프로그램과 서버 사이에서 전송될 때 변환되지 않습니다. 클라이언트 컴퓨터는 코드 ACP (ANSI 페이지) SQL Server 코드 페이지와에서 다른을 사용 하는 경우 ANSI 문자열의 확장된 문자가 잘못 해석 될 수 있습니다. 클라이언트 컴퓨터는 동일한 코드 페이지를 사용 하는 SQL Server를 사용 하는 acp, 경우 확장된 문자는 올바르게 해석 됩니다.

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>통화, 숫자, 날짜 및 시간 표기에 국가별 설정 사용

드라이버가 문자 출력 문자열의 통화, 숫자, 날짜 및 시간에 서식을 지정할 때 클라이언트 컴퓨터의 국가별 설정을 사용하도록 지정합니다. 드라이버는 데이터 원본을 통해 연결된 사용자의 Windows 로그인 계정에 대한 기본 국가별 설정을 사용합니다. 데이터를 처리하지 않고 단순히 표시하기만 하는 응용 프로그램에 대해 이 옵션을 선택하십시오.

### <a name="save-long-running-queries-to-the-log-file"></a>장기 실행 쿼리를 다음 로그 파일에 저장

해당 드라이버 로그 보다 더 오래 걸리는 모든 쿼리를 지정 된 **장기 쿼리 시간** 값입니다. 장기 실행 쿼리는 지정된 파일에 기록됩니다. 로그 파일을 지정 하려면 상자에 전체 경로 파일 이름을 입력 하거나 클릭 **찾아보기** 를 기존 파일 디렉터리를 통해 이동 하 여 로그 파일을 선택 합니다.

### <a name="long-query-time-milliseconds"></a>장기 쿼리 시간(밀리초)

장기 실행 쿼리 기록을 위한 임계값을 밀리초 단위로 지정합니다. 지정된 시간(밀리초)보다 오랫동안 실행되는 모든 쿼리가 기록됩니다.

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>ODBC 드라이버 통계를 다음 로그 파일에 기록

통계를 기록하도록 지정합니다. 통계는 지정된 파일에 기록됩니다. 로그 파일을 지정 하려면 중 하나에 전체 경로 파일 이름을 입력 하거나 클릭 **찾아보기** 를 기존 파일 디렉터리를 통해 이동 하 여 로그 파일을 선택 합니다.

통계 로그는 탭으로 구분된 파일이며, Microsoft Excel 또는 탭으로 구분된 파일을 지원하는 기타 응용 프로그램으로 분석할 수 있습니다.

### <a name="connect-retry-count"></a>연결 다시 시도 횟수

시도가 실패 한 연결을 다시 시도 횟수를 지정 합니다.

### <a name="connect-retry-interval-seconds"></a>연결 다시 시도 간격 (초)

각 연결 다시 시도 간격 (초)을 지정합니다. 이 작업에 대 한 자세한 내용은 및 **연결 다시 시도 횟수가** 옵션 참조 [Windows ODBC 드라이버에서 연결 복원 력](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)합니다.

### <a name="back"></a>뒤로

마법사의 이전 페이지로 이동 하려면이 단추를 클릭 합니다.

### <a name="finish"></a>마침

이 화면에 지정 된 정보를 완료 하는 경우 클릭할 수 있는 **마침**합니다. DSN이 고, 마법사의 다른 화면에 지정 된 모든 특성을 사용 하 여 만들어지고를 테스트할 새로 만든 DSN 사항이 있습니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 3](../../../connect/odbc/windows/dsn-wizard-3.md)
