---
title: Linux 및 macOS에서 ODBC 드라이버를 사용하여 데이터 액세스 추적 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fa39cd11f70a661de5c284e56f2ccc0f7a5777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008826"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Linux 및 macOS에서 ODBC 드라이버를 사용하여 데이터 액세스 추적

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

MacOS 및 Linux의 총 Xodbc 드라이버 관리자는 ODBC API 호출 항목 추적 및 용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]odbc 드라이버 종료를 지원 합니다.

응용 프로그램의 ODBC 동작 `odbcinst.ini` 을 추적 하려면 파일의 `[ODBC]` 섹션을 편집 하 여 값 `Trace=Yes` 과 `TraceFile` 추적 출력을 포함 하는 파일의 경로를 설정 합니다. 예를 들면 다음과 같습니다.

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

또는 다른 장치 이름을 사용 `/dev/stdout` 하 여 영구 파일 대신 추적 출력을 보낼 수도 있습니다. 위의 설정을 사용 하는 경우 응용 프로그램에서 전체 Xodbc 드라이버 관리자를 로드할 때마다 출력 파일에 수행 된 모든 ODBC API 호출이 기록 됩니다.

응용 프로그램 추적을 마친 후에는 `Trace=Yes` `odbcinst.ini` 파일에서를 제거 하 여 추적의 성능 저하를 방지 하 고 불필요 한 추적 파일이 제거 되었는지 확인 합니다.

추적은 `odbcinst.ini`에서 드라이버를 사용하는 모든 애플리케이션에 적용됩니다. 일부 애플리케이션을 추적하지 않으려면(예: 중요한 사용자별 정보가 공개되는 것을 방지하려는 경우) `ODBCSYSINI` 환경 변수를 사용하여 프라이빗 `odbcinst.ini`의 위치를 제공함으로써 개별 애플리케이션 인스턴스를 추적할 수 있습니다. 예를 들어

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

이 경우의 `Trace=Yes` `[ODBC Driver 13 for SQL Server]` 섹션에를추가할수있습니다`/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>드라이버가 사용 중인 odbc.ini 파일 확인

Linux 및 macos ODBC 드라이버는 사용 중인 `odbc.ini` `odbc.ini` 파일 또는 파일 경로를 알 수 없습니다. 그러나 사용 중인 `odbc.ini` 파일에 대 한 정보는 모든 파일에 대 한 정보를 사용할 수 `odbcinst`있습니다 `odbc_config` .

예를 들어 다음 명령은 (기타 정보 중) 각각 시스템 및 사용자 DSN이 포함된 시스템 및 사용자 `odbc.ini` 파일의 위치를 인쇄합니다.

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

이 [문서](http://www.unixodbc.org/doc/UserManual/) 에서는 사용자와 시스템 dsn 간의 차이점에 대해 설명 합니다. 요약:

- 사용자 Dsn---특정 사용자만 사용할 수 있는 Dsn입니다. 사용자는 자신의 사용자 Dsn을 사용 하 여 연결, 추가, 수정 및 제거할 수 있습니다. 사용자 Dsn은 사용자의 홈 디렉터리 또는 하위 디렉터리의 파일에 저장 됩니다.

- 이러한 Dsn---시스템 Dsn은 시스템의 모든 사용자가 사용 하 여 연결할 수 있지만 시스템 관리자만 추가, 수정 및 제거할 수 있습니다. 사용자에 게 시스템 DSN과 동일한 이름의 사용자 DSN이 있는 경우 해당 사용자의 연결에 사용자 DSN이 사용 됩니다.

## <a name="see-also"></a>참고 항목

- [프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)
