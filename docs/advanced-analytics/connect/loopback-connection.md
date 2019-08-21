---
title: Python 또는 R 스크립트에서 SQL Server에 대 한 루프백 연결
description: 루프백 연결을 사용 하 여 sp_execute_external_script에서 실행 되는 Python 또는 R 스크립트에서 데이터를 읽거나 쓰기 위해 ODBC를 통해 SQL Server에 다시 연결 하는 방법에 대해 알아봅니다. Sp_execute_external_script의 InputDataSet 및 OutputDataSet 인수를 사용할 수 없는 경우이를 사용할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2019
ms.topic: conceptual
author: Aniruddh25
ms.author: anmunde
ms.reviewer: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 62b4ce483df2d38e5e2549d054c02b6c797837f3
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69657490"
---
# <a name="loopback-connection-to-sql-server-from-a-python-or-r-script"></a>Python 또는 R 스크립트에서 SQL Server에 대 한 루프백 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

루프백 연결을 사용 하 여 [ODBC](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md) 를 통해 SQL Server에 다시 연결 하 여에서 `sp_execute_external_script`실행 되는 Python 또는 R 스크립트에서 데이터를 읽거나 쓰는 방법을 알아봅니다. **Inputdataset** 및 **outputdataset** 인수 `sp_execute_external_script` 를 사용할 수 없는 경우이를 사용할 수 있습니다.

## <a name="connection-string"></a>연결 문자열

루프백 연결을 설정 하려면 올바른 연결 문자열을 사용 해야 합니다. 일반적인 필수 인수는 [ODBC 드라이버](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)의 이름, 서버 주소 및 데이터베이스의 이름입니다.

### <a name="connection-string-on-windows"></a>Windows의 연결 문자열

Windows에서 SQL Server에 대 한 인증의 경우 Python 또는 R 스크립트는 **Trusted_Connection** 연결 문자열 특성을 사용 하 여 sp_execute_external_script를 실행 한 것과 동일한 사용자로 인증할 수 있습니다.

Windows에 대 한 루프백 연결 문자열의 예는 다음과 같습니다.

``` 
"Driver=SQL Server;Server=.;Database=nameOfDatabase;Trusted_Connection=Yes;"
```

### <a name="connection-string-on-linux"></a>Linux의 연결 문자열

SQL Server on Linux에 대 한 인증의 경우 Python 또는 R 스크립트는 ODBC 드라이버의 **ClientCertificate** 및 **clientkey** 특성을 사용 하 여를 실행 `sp_execute_external_script`한 것과 동일한 사용자로 인증 해야 합니다. 이를 위해서는 [최신 ODBC 드라이버](../../connect/odbc/download-odbc-driver-for-sql-server.md) 버전 17.4.1.1을 사용 해야 합니다.

Linux에 대 한 루프백 연결 문자열의 예는 다음과 같습니다.

```
"Driver=ODBC Driver 17 for SQL Server;Server=fe80::8012:3df5:0:5db1%eth0;Database=nameOfDatabase;ClientCertificate=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitecert.pem;ClientKey=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitekey.pem;TrustServerCertificate=Yes;Trusted_Connection=no;Encrypt=Yes"
```

서버 주소, 클라이언트 인증서 파일 위치 및 클라이언트 키 파일 위치는 각각 `sp_execute_external_script` 에 고유 하며 Python **용 API rx_get_sql_loopback_connection_string ()를 사용 하 여 가져올 수 있습니다.** R에 대 한 rxGetSqlLoopbackConnectionString ()입니다.

연결 문자열 특성에 대 한 자세한 내용은 [DSN 및 연결 문자열 키워드 및](https://docs.microsoft.com/sql/connect/odbc/dsn-connection-string-attribute?view=sql-server-linux-ver15#new-connection-string-keywords-and-connection-attributes) Microsoft ODBC Driver for SQL Server에 대 한 특성을 참조 하세요.

## <a name="generate-connection-string-with-revoscalepy-for-python"></a>Python 용 revoscalepy를 사용 하 여 연결 문자열 생성

[Revoscalepy](../python/ref-py-revoscalepy.md) 에서 API **rx_get_sql_loopback_connection_string ()** 를 사용 하 여 Python 스크립트에서 루프백 연결에 대 한 올바른 연결 문자열을 생성할 수 있습니다.

다음 인수를 허용 합니다.

| 인수 | 설명 |
|-|-|
| name_of_database | 연결을 설정할 데이터베이스의 이름입니다. |
| odbc_driver | Odbc 드라이버의 이름입니다. |

### <a name="examples"></a>예

Windows의 SQL Server에 대 한 예제:

```sql
EXECUTE sp_execute_external_script
@language = N'Python',
@script = N'
from revoscalepy import rx_get_sql_loopback_connection_string, RxSqlServerData, rx_data_step
loopback_connection_string = rx_get_sql_loopback_connection_string(odbc_driver="SQL Server", name_of_database="DBName")
print("Connection String:{0}".format(loopback_connection_string))
data_set = RxSqlServerData(sql_query = "select col1, col2 from tableName",
                           connection_string = loopback_connection_string)
OutputDataSet = rx_data_step(data_set)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

SQL Server on Linux에 대 한 예제:

```sql
EXECUTE sp_execute_external_script
@language = N'Python',
@script = N'
from revoscalepy import rx_get_sql_loopback_connection_string, RxSqlServerData, rx_data_step
loopback_connection_string = rx_get_sql_loopback_connection_string(odbc_driver="ODBC Driver 17 for SQL Server",
                                                                   name_of_database="DBName")
print("Loopback Connection String:{0}".format(loopback_connection_string))
data_set = RxSqlServerData(sql_query = "select col1, col2 from tableName",
                           connection_string = loopback_connection_string)
OutputDataSet = rx_data_step(data_set)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

## <a name="generate-connection-string-with-revoscaler-for-r"></a>R에 대해 RevoScaleR를 사용 하 여 연결 문자열 생성

[RevoScaleR](../r/ref-r-revoscaler.md) 의 API **rxGetSqlLoopbackConnectionString ()** 를 사용 하 여 R 스크립트에서 루프백 연결에 대 한 올바른 연결 문자열을 생성할 수 있습니다.

다음 인수를 허용 합니다.

| 인수 | 설명 |
|-|-|
| nameOfDatabase | 연결을 설정할 데이터베이스의 이름입니다. |
| odbcDriver | Odbc 드라이버의 이름입니다. |

### <a name="examples"></a>예

Windows의 SQL Server에 대 한 예제:

```sql
EXECUTE sp_execute_external_script
@language = N'R',
@script = N'
    loopbackConnectionString <- rxGetSqlLoopbackConnectionString(nameOfDatabase="DBName", odbcDriver ="SQL Server")
    print(paste("Connection String:", loopbackConnectionString))
    dataSet <- RxSqlServerData(sqlQuery = "select col1, col2 from tableName",
                               connectionString = loopbackConnectionString)
    OutputDataSet <- rxDataStep(dataSet)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

SQL Server on Linux에 대 한 예제:

```sql
EXECUTE sp_execute_external_script
@language = N'R',
@script = N'
    loopbackConnectionString <-  rxGetSqlLoopbackConnectionString(nameOfDatabase="DBName", 
                                                                  odbcDriver ="ODBC Driver 17 for SQL Server")
    print(paste("Connection String:", loopbackConnectionString))
    dataSet <- RxSqlServerData(sqlQuery = "select col1, col2 from tableName", 
                               connectionString = loopbackConnectionString)
    OutputDataSet <- rxDataStep(dataSet)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

## <a name="next-steps"></a>다음 단계

+ [SQL Server 용 Microsoft ODBC 드라이버](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)
+ [revoscalepy](../python/ref-py-revoscalepy.md)
+ [RevoScaleR](../r/ref-r-revoscaler.md)
