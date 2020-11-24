---
title: SQL 테이블 데이터를 Python pandas 데이터 프레임에 삽입
titleSuffix: SQL machine learning
description: Python을 사용하여 SQL 테이블에서 데이터를 읽고 pandas 데이터 프레임에 삽입하는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 07/23/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: 041291804f6fbefe4832398b7c56b2ab97940008
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870248"
---
# <a name="insert-data-from-a-sql-table-into-a-python-pandas-dataframe"></a>SQL 테이블 데이터를 Python pandas 데이터 프레임에 삽입
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

이 문서에서는 Python에서 [pyodbc](../../connect/python/pyodbc/python-sql-driver-pyodbc.md) 패키지를 사용하여 [pandas](https://pandas.pydata.org/) 데이터 프레임에 SQL 데이터를 삽입하는 방법을 설명합니다. 데이터 프레임에 포함된 데이터의 행과 열을 추가 데이터 탐색에 사용할 수 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* [Windows용 SQL Server](../../database-engine/install-windows/install-sql-server.md) 또는 [Linux용 SQL Server](../../linux/sql-server-linux-overview.md)
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
* [Azure SQL Database](/azure/sql-database/sql-database-get-started-portal)
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/instance-create-quickstart)

* 샘플 데이터베이스를 Azure SQL Managed Instance로 복원하기 위한 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md).
::: moniker-end

* Azure Data Studio. 설치하려면 [Azure Data Studio](../../azure-data-studio/what-is.md)를 참조하세요.

* [샘플 데이터베이스를 복원](../../samples/adventureworks-install-configure.md)하여 이 문서에서 사용되는 샘플 데이터를 가져옵니다.

## <a name="verify-restored-database"></a>복원된 데이터베이스 확인

**Person.CountryRegion** 테이블을 쿼리하여 복원된 데이터베이스가 있는지 확인할 수 있습니다.

```sql
USE AdventureWorks;
SELECT * FROM Person.CountryRegion;
```

## <a name="install-python-packages"></a>Python 패키지 설치

[Azure Data Studio를 다운로드 및 설치](../../azure-data-studio/download-azure-data-studio.md)합니다.

다음 Python 패키지를 설치합니다.
  * pyodbc
  * pandas

  이러한 패키지를 설치하려면

  1. Azure Data Studio Notebook에서 **패키지 관리** 를 선택합니다.
  2. **패키지 관리** 창에서 **새로 추가** 탭을 선택합니다.
  3. 다음 패키지 각각에 대해 패키지 이름을 입력하고 **검색** 을 클릭한 다음 **설치** 를 클릭합니다.

## <a name="insert-data"></a>데이터 삽입

다음 스크립트를 사용하여 Person.CountryRegion 테이블에서 데이터를 선택하고 데이터 프레임에 삽입합니다. SQL에 연결하기 위한 연결 문자열 변수 'server', 'database', 'username' 및 'password'를 편집합니다.

새 Notebook을 만들려면:

1. Azure Data Studio에서 **파일** 을 선택하고 **새 Notebook** 을 선택합니다.
2. Notebook에서 커널 **Python3** 를 선택하고 **+code** 를 선택합니다.
3. Notebook에 코드를 붙여넣고 **모두 실행** 을 선택합니다.

```python
import pyodbc
import pandas as pd
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorks' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
# select 26 rows from SQL table to insert in dataframe.
query = "SELECT [CountryRegionCode], [Name] FROM Person.CountryRegion;"
df = pd.read_sql(query, cnxn)
print(df.head(26))
```

**출력**

이전 스크립트의 `print` 명령은 `pandas` 데이터 프레임 `df`의 데이터 행을 표시합니다.

```text
CountryRegionCode                 Name
0                 AF          Afghanistan
1                 AL              Albania
2                 DZ              Algeria
3                 AS       American Samoa
4                 AD              Andorra
5                 AO               Angola
6                 AI             Anguilla
7                 AQ           Antarctica
8                 AG  Antigua and Barbuda
9                 AR            Argentina
10                AM              Armenia
11                AW                Aruba
12                AU            Australia
13                AT              Austria
14                AZ           Azerbaijan
15                BS         Bahamas, The
16                BH              Bahrain
17                BD           Bangladesh
18                BB             Barbados
19                BY              Belarus
20                BE              Belgium
21                BZ               Belize
22                BJ                Benin
23                BM              Bermuda
24                BT               Bhutan
25                BO              Bolivia
```

## <a name="next-steps"></a>다음 단계

+ [SQL에 Python 데이터 프레임 삽입](../data-exploration/python-dataframe-sql-server.md)