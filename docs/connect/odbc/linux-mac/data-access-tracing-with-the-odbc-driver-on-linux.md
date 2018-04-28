---
title: Linux와 macOS에서 ODBC 드라이버를 사용 하 여 데이터 액세스 추적 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4fadd1ddbcf4004b3a6652975c2495db9007d433
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Linux와 macOS에서 ODBC 드라이버를 사용 하 여 데이터 액세스 추적
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

MacOS 및 Linux에서 unixODBC 드라이버 관리자 추적의 ODBC API 호출 진입 및 종료에 대 한 ODBC 드라이버의 지원 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.

응용 프로그램의 ODBC 동작을 추적 하려면 편집는 `odbcinst.ini` 파일의 `[ODBC]` 값을 설정 하는 섹션 `Trace=Yes` 및 `TraceFile` 추적; 출력을 포함 하는 파일의 경로를 예:

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(사용할 수 있습니다 `/dev/stdout` 또는 다른 장치 이름 대신 영구 파일에 있는 출력 추적을 보내도록 합니다.) 위의 설정을 사용 하 여 응용 프로그램에 unixODBC 드라이버 관리자를 로드 될 때마다 기록지 않습니다을 출력 파일에 수행한 모든 ODBC API 호출 합니다.

응용 프로그램 추적을 마친 후 제거 `Trace=Yes` 에서 `odbcinst.ini` 추적의 성능 저하를 방지 하기 위해 파일을 불필요 한 추적 파일이 제거 되었는지 확인 합니다.
  
추적에서 드라이버를 사용 하는 모든 응용 프로그램에 적용 됩니다. `odbcinst.ini`합니다. 모든 응용 프로그램 (예: 중요 한 사용자 정보를 공개 하지 않으려면)을 추적 하지, 개인의 위치를 제공 하 여 개별 응용 프로그램 인스턴스를 추적할 수 `odbcinst.ini`를 사용 하 여는 `ODBCSYSINI` 환경 변수입니다. 예를 들어:  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
이 경우 추가할 수 있습니다 `Trace=Yes` 에 `[ODBC Driver 13 for SQL Server]` 섹션 `/home/myappuser/odbcinst.ini`합니다.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>드라이버에서 사용 중인 어느 odbc.ini 파일 확인

Linux와 macOS ODBC 드라이버 알지 못하면 `odbc.ini` 사용 또는에 대 한 경로는 `odbc.ini` 파일입니다. 그러나 정보에 대 한 `odbc.ini` 파일은 사용 되는 unixODBC 도구에서 사용할 수 있는 `odbc_config` 및 `odbcinst`, unixODBC 드라이버 관리자 설명서에서.  
  
예를 들어 다음 명령은 인쇄 (기타 정보 중) 시스템 및 사용자의 위치 `odbc.ini` 사용자 Dsn 및 시스템 각각 포함 된 파일:

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

[unixODBC 설명서](http://www.unixodbc.org/doc/UserManual/) 사용자 및 시스템 Dsn 차이점에 설명 합니다. 요약:  

- 사용자 Dsn---이들은 특정 사용자에 게 사용할 수 있는 Dsn입니다. 사용자가 사용 하 여 연결, 추가, 수정 하 고 수 자신의 사용자 Dsn를 제거 합니다. 사용자 Dsn이 사용자의 홈 디렉터리 또는 해당 하위 디렉터리의 파일에 저장 됩니다.
  
- 시스템 Dsn---이 Dsn,를 사용 하 여 연결 하려면 시스템에서 모든 사용자에 대해 사용할 수 있지만 수만 추가, 수정 및 시스템 관리자에 의해 제거 합니다. 사용자는 시스템 DSN으로 같은 이름의 사용자 DSN, 해당 사용자가 사용자 DSN 연결 시 사용 됩니다.

## <a name="see-also"></a>관련 항목:
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)
