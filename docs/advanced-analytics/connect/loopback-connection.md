---
title: SQL 루프백 연결
description: 루프백 연결을 사용해서 ODBC로 SQL Server에 다시 연결하여 sp_execute_external_script로부터 실행된 Python 또는 R 스크립트에서 데이터를 읽거나 쓰는 방법을 알아봅니다. 이 방법은 sp_execute_external_script의 InputDataSet 및 OutputDataSet 인수를 사용할 수 없을 때 사용할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2019
ms.topic: conceptual
author: Aniruddh25
ms.author: anmunde
ms.reviewer: dphansen
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c7fa36db48a7912951f0232136945798caf6f7f7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727594"
---
# <a name="loopback-connection-to-sql-server-from-a-python-or-r-script"></a>Python 또는 R 스크립트에서 SQL Server에 루프백 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

루프백 연결을 사용해서 [ODBC](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)로 SQL Server에 다시 연결하여 `sp_execute_external_script`로부터 실행된 Python 또는 R 스크립트에서 데이터를 읽거나 쓰는 방법을 알아봅니다. 이 방법은 **의** InputDataSet**및**OutputDataSet`sp_execute_external_script` 인수 사용이 불가능할 때 사용할 수 있습니다.

## <a name="connection-string"></a>연결 문자열

루프백 연결을 위해서는 올바른 연결 문자열을 사용해야 합니다. 일반적인 필수 인수는 [ODBC 드라이버](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)의 이름, 서버 주소 및 데이터베이스의 이름입니다.

### <a name="connection-string-on-windows"></a>Windows에 대한 연결 문자열

Windows에서 SQL Server 인증을 위해 Python 또는 R 스크립트는 **Trusted_Connection** 연결 문자열 특성을 사용하여 sp_execute_external_script를 실행한 동일한 사용자로 인증할 수 있습니다.

Windows에서 루프백 연결 문자열 예는 다음과 같습니다.

``` 
"Driver=SQL Server;Server=.;Database=nameOfDatabase;Trusted_Connection=Yes;"
```

### <a name="connection-string-on-linux"></a>Linux에 대한 연결 문자열

Linux에서 SQL Server 인증을 위해서는 Python 또는 R 스크립트가 ODBC 드라이버의 **ClientCertificate** 및 **ClientKey** 특성을 사용하여 `sp_execute_external_script`를 실행한 동일한 사용자로 인증해야 합니다. 이를 위해서는 [최신 ODBC 드라이버](../../connect/odbc/download-odbc-driver-for-sql-server.md) 버전 17.4.1.1을 사용해야 합니다.

Linux에서 루프백 연결 문자열 예는 다음과 같습니다.

```
"Driver=ODBC Driver 17 for SQL Server;Server=fe80::8012:3df5:0:5db1%eth0;Database=nameOfDatabase;ClientCertificate=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitecert.pem;ClientKey=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitekey.pem;TrustServerCertificate=Yes;Trusted_Connection=no;Encrypt=Yes"
```

서버 주소, 클라이언트 인증서 파일 위치 및 클라이언트 키 파일 위치는 모든 `sp_execute_external_script`에 대해 고유하며, Python의 경우 API **rx_get_sql_loopback_connection_string()** , R의 경우에는 **rxGetSqlLoopbackConnectionString()** 을 사용하여 얻을 수 있습니다.

연결 문자열 특성에 대한 자세한 내용은 Microsoft ODBC Driver for SQL Server에 대한 [DSN 및 연결 문자열 키워드 및 특성](https://docs.microsoft.com/sql/connect/odbc/dsn-connection-string-attribute?view=sql-server-linux-ver15#new-connection-string-keywords-and-connection-attributes)을 참조하십시오.

## <a name="generate-connection-string-with-revoscalepy-for-python"></a>Python용 revoscalepy를 사용하여 연결 문자열 생성

**revoscalepy**에서 API [rx_get_sql_loopback_connection_string()](../python/ref-py-revoscalepy.md)을 사용하여 Python 스크립트에서 루프백 연결을 위해 올바른 연결 문자열을 생성할 수 있습니다.

다음 인수가 사용됩니다.

| 인수 | Description |
|-|-|
| name_of_database | 연결을 설정할 데이터베이스 이름입니다. |
| odbc_driver | ODBC 드라이버의 이름입니다. |

### <a name="examples"></a>예

Windows의 SQL Server 예:

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

Linux의 SQL Server 예:

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

## <a name="generate-connection-string-with-revoscaler-for-r"></a>R용 RevoScaleR을 사용하여 연결 문자열 생성

**RevoScaleR**에서 API [rxGetSqlLoopbackConnectionString()](../r/ref-r-revoscaler.md)을 사용하여 R 스크립트에서 루프백 연결을 위해 올바른 연결 문자열을 생성할 수 있습니다.

다음 인수가 사용됩니다.

| 인수 | Description |
|-|-|
| nameOfDatabase | 연결을 설정할 데이터베이스 이름입니다. |
| odbcDriver | ODBC 드라이버의 이름입니다. |

### <a name="examples"></a>예

Windows의 SQL Server 예:

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

Linux의 SQL Server 예:

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

+ [Microsoft ODBC driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)
+ [revoscalepy](../python/ref-py-revoscalepy.md)
+ [RevoScaleR](../r/ref-r-revoscaler.md)
