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
manager: craigg
ms.openlocfilehash: 5cd3795f57f544d5f7003f7aab60be2a08a64229
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607193"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Linux 및 macOS에서 ODBC 드라이버를 사용하여 데이터 액세스 추적
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

MacOS 및 Linux에서 unixODBC 드라이버 관리자 추적을 ODBC API 호출 진입 및 종료에 대 한 ODBC 드라이버의 지원 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.

응용 프로그램의 ODBC 동작을 추적 하려면 편집 합니다 `odbcinst.ini` 파일의 `[ODBC]` 값을 설정 하는 섹션 `Trace=Yes` 및 `TraceFile` ; 출력 추적을 포함 하는 파일의 경로를 예를 들어:

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(사용할 수도 있습니다 `/dev/stdout` 또는 다른 장치 이름 대신 영구 파일에 있는 출력 추적을 보내도록 합니다.) UnixODBC 드라이버 관리자를 로드 하는 응용 프로그램 때마다 위의 설정을 사용 하 여 출력 파일에 수행 하는 모든 ODBC API 호출을 기록 합니다 것입니다.

응용 프로그램 추적을 마친 후 제거 `Trace=Yes` 에서 `odbcinst.ini` 추적의 성능 저하를 방지 하려면 파일 및 불필요 한 추적 파일 제거 되었는지 확인 하십시오.
  
추적은 `odbcinst.ini`에서 드라이버를 사용하는 모든 응용 프로그램에 적용됩니다. 일부 응용 프로그램을 추적하지 않으려면(예: 중요한 사용자별 정보가 공개되는 것을 방지하려는 경우) `ODBCSYSINI` 환경 변수를 사용하여 비공개 `odbcinst.ini`의 위치를 제공함으로써 개별 응용 프로그램 인스턴스를 추적할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
이 경우에 추가할 수 있습니다 `Trace=Yes` 에 `[ODBC Driver 13 for SQL Server]` 부분 `/home/myappuser/odbcinst.ini`합니다.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>드라이버가 사용 중인 odbc.ini 파일 확인

Linux 및 macOS ODBC 드라이버 알지 못하면 `odbc.ini` 사용에 대 한 경로는 `odbc.ini` 파일입니다. 그러나에 대 한 정보 `odbc.ini` 파일은 unixODBC 도구에서 사용 가능 `odbc_config` 및 `odbcinst`, 및 unixODBC 드라이버 관리자 설명서.  
  
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

합니다 [unixODBC 설명서](https://www.unixodbc.org/doc/UserManual/) 사용자 및 시스템 Dsn 간의 차이점을 설명 합니다. 요약:  

- 사용자 Dsn---이들은 에서만 특정 사용자에 게 제공 되는 Dsn입니다. 사용자가 사용 하 여 연결, 추가, 수정 및 제거할 수는 자신의 사용자 Dsn입니다. 사용자 Dsn이 사용자의 홈 디렉터리, 또는 그 하위 디렉터리의 파일에 저장 됩니다.
  
- 시스템 Dsn---이 Dsn은 사용 하 여 연결할 시스템에서 모든 사용자에 대해 사용할 수 있지만 추가, 수정 하 고 제거할 수 시스템 관리자가 합니다. 사용자에 게 시스템 DSN으로 같은 이름의 사용자 DSN에 하는 경우 해당 사용자가 사용자 DSN 연결 시 사용 됩니다.

## <a name="see-also"></a>참고 항목
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)
