---
title: SQL 테이블에 Python 데이터 프레임 삽입
titleSuffix: SQL machine learning
description: 데이터 프레임에서 SQL 테이블로 데이터를 삽입하는 방법입니다.
author: cawrites
ms.author: chadam
ms.date: 07/23/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: f479186a8b1455fab8e8ddac7313193337e42dc9
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956843"
---
# <a name="insert-python-dataframe-into-sql-table"></a>SQL 테이블에 Python 데이터 프레임 삽입
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

이 문서에서는 Python에서 [pyodbc](../../connect/python/pyodbc/python-sql-driver-pyodbc.md) 패키지를 사용하여 SQL 데이터베이스에 [pandas](https://pandas.pydata.org/) 데이터 프레임을 삽입하는 방법을 설명합니다.

## <a name="prerequisites"></a>필수 구성 요소

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* SQL Server. 설치 방법은 [Windows용 SQL Server](../../database-engine/install-windows/install-sql-server.md) 또는 [Linux용 SQL Server](../../linux/sql-server-linux-overview.md)를 참조하세요.
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
* Azure SQL Database. 등록 방법은 [Azure SQL Database](/azure/sql-database/sql-database-get-started-portal)를 참조하세요.
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Azure SQL Managed Instance. 등록 방법은 [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/instance-create-quickstart)를 참조하세요.

* 샘플 데이터베이스를 Azure SQL Managed Instance로 복원하기 위한 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md).
::: moniker-end

* Azure Data Studio. 설치 방법은 [Azure Data Studio](../../azure-data-studio/what-is.md)를 참조하세요.

* [샘플 데이터베이스를 복원](../../samples/adventureworks-install-configure.md)하여 이 문서에서 사용되는 샘플 데이터를 가져옵니다.

## <a name="verify-restored-database"></a>복원된 데이터베이스 확인

**HumanResources.Department** 테이블을 쿼리하여 복원된 데이터베이스가 있는지 확인할 수 있습니다.

```sql
USE AdventureWorks;
SELECT * FROM HumanResources.Department;
```

## <a name="install-python-packages"></a>Python 패키지 설치

* [Azure Data Studio 다운로드 및 설치](../../azure-data-studio/download-azure-data-studio.md)

다음 Python 패키지를 설치합니다.
  * pyodbc
  * pandas

  이러한 패키지를 설치하려면

  1. Azure Data Studio Notebook에서 **패키지 관리**를 선택합니다.
  2. **패키지 관리** 창에서 **새로 추가** 탭을 선택합니다.
  3. 다음 패키지 각각에 대해 패키지 이름을 입력하고 **검색**을 클릭한 다음 **설치**를 클릭합니다.

## <a name="connect-to-sql-server-using-azure-data-studio"></a>Azure Data Studio를 사용하여 SQL Server에 연결

[Azure Data Studio를 사용하여 연결](../../azure-data-studio/quickstart-sql-server.md)합니다.

1. Adventureworks 데이터베이스에 연결하여 새 테이블 HumanResources.DepartmentTest를 만듭니다. 이 SQL 테이블은 데이터 프레임 삽입에 사용됩니다.

```sql
CREATE TABLE [HumanResources].[DepartmentTest](
[DepartmentID] [smallint] NOT NULL,
[Name] [dbo].[Name] NOT NULL,
[GroupName] [dbo].[Name] NOT NULL
)
GO
```

## <a name="create-csv-file"></a>CSV 파일 만들기

데이터 프레임을 위해 텍스트를 복사하고 파일을 department.csv로 저장합니다.

```text
DepartmentID,Name,GroupName,
1,Engineering,Research and Development,
2,Tool Design,Research and Development,
3,Sales,Sales and Marketing,
4,Marketing,Sales and Marketing,
5,Purchasing,Inventory Management,
6,Research and Development,Research and Development,
7,Production,Manufacturing,
8,Production Control,Manufacturing,
9,Human Resources,Executive General and Administration,
10,Finance,Executive General and Administration,
11,Information Services,Executive General and Administration,
12,Document Control,Quality Assurance,
13,Quality Assurance,Quality Assurance,
14,Facilities and Maintenance,Executive General and Administration,
15,Shipping and Receiving,Inventory Management,
16,Executive,Executive General and Administration
```

## <a name="connect-to-sql-using-python"></a>Python을 사용하여 SQL에 연결

1. SQL 데이터베이스에 연결하기 위한 연결 문자열 변수 'server', 'database', 'username' 및 'password'를 편집합니다.

2. CSV 파일의 경로를 편집합니다.

## <a name="load-dataframe-from-csv-file"></a>CSV 파일에서 데이터 프레임 로드

Python `pandas` 패키지를 사용하여 데이터 프레임을 만들고 CSV 파일을 로드합니다. SQL에 연결하여 데이터 프레임을 새 SQL 테이블 HumanResources.DepartmentTest로 로드합니다.

새 Notebook을 만들려면:

1. Azure Data Studio에서 **파일**을 선택하고 **새 Notebook**을 선택합니다.
2. Notebook에서 커널 **Python3**를 선택하고 **+code**를 선택합니다.
3. Notebook에 코드를 붙여넣고 **모두 실행**을 선택합니다.

 ```Python
import pyodbc
import pandas as pd
# insert data from csv file into dataframe.
# working directory for csv file: type "pwd" in Azure Data Studio or Linux
# working directory in Windows c:\users\username
df = pd.read_csv("c:\\user\\username\department.csv")
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'yourservername' 
database = 'AdventureWorks' 
username = 'username' 
password = 'yourpassword' 
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
# Insert Dataframe into SQL Server:
for index, row in df.iterrows():
     cursor.execute("INSERT INTO HumanResources.DepartmentTest (DepartmentID,Name,GroupName) values(?,?,?)", row.DepartmentID, row.Name, row.GroupName)
cnxn.commit()
cursor.close()
```

## <a name="confirm-row-count-in-sql"></a>SQL에서 행 수 확인

SQL 문을 실행하여 데이터 프레임의 데이터가 테이블에 성공적으로 로드되었는지 확인합니다.

```sql
SELECT count(*) from HumanResources.DepartmentTest;
```

결과

```bash
(No column name)
16
```

## <a name="next-steps"></a>다음 단계

+ [Python을 사용하여 데이터 탐색을 위한 히스토그램 그리기](../data-exploration/python-plot-histogram.md)