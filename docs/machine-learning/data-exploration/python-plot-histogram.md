---
title: Python을 사용하여 데이터 탐색을 위한 히스토그램 그리기
titleSuffix: SQL machine learning
description: Python을 사용하여 데이터를 시각화하는 히스토그램을 만드는 방법을 알아봅니다.
author: cawrites
ms.author: chadam
ms.date: 07/14/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: c1f30230b00258b5f5f662a99c2d75c29ea7ba8d
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956810"
---
# <a name="plot-histograms-in-python"></a>Python에서 히스토그램 그리기 
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

이 문서에서는 Python 패키지 [pandas'.hist()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.hist.html)를 사용하여 데이터를 그리는 방법을 설명합니다. SQL 데이터베이스가 중복되지 않는 연속 값이 포함된 히스토그램 데이터 간격을 시각화하는 데 사용되는 원본입니다.

## <a name="prerequisites"></a>필수 조건:

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

* [샘플 DW 데이터베이스를 복원](../../samples/adventureworks-install-configure.md)하여 이 문서에서 사용되는 샘플 데이터를 가져옵니다.

## <a name="verify-restored-database"></a>복원된 데이터베이스 확인

**Person.CountryRegion** 테이블을 쿼리하여 복원된 데이터베이스가 있는지 확인할 수 있습니다.
```sql
USE AdventureWorksDW;
SELECT * FROM Person.CountryRegion;
```
  
## <a name="install-python-packages"></a>Python 패키지 설치

[Azure Data Studio를 다운로드 및 설치](../../azure-data-studio/download-azure-data-studio.md)합니다.

다음 Python 패키지를 설치합니다.
  * pyodbc
  * pandas

  이러한 패키지를 설치하려면

  1. Azure Data Studio Notebook에서 **패키지 관리**를 선택합니다.
  2. **패키지 관리** 창에서 **새로 추가** 탭을 선택합니다.
  3. 다음 패키지 각각에 대해 패키지 이름을 입력하고 **검색**을 클릭한 다음 **설치**를 클릭합니다.

## <a name="plot-histogram"></a>히스토그램 그리기

히스토그램에 표시되는 분산 데이터는 AdventureWorksDW의 SQL 쿼리를 기반으로 합니다. 이 히스토그램은 데이터와 데이터 값 빈도를 시각화합니다. SQL 데이터베이스에 연결하기 위한 연결 문자열 변수 'server', 'database', 'username' 및 'password'를 편집합니다.

새 Notebook을 만들려면:

1. Azure Data Studio에서 **파일**을 선택하고 **새 Notebook**을 선택합니다.
2. Notebook에서 커널 **Python3**를 선택하고 **+code**를 선택합니다.
3. Notebook에 코드를 붙여넣고 **모두 실행**을 선택합니다.

```python
import pyodbc 
import pandas as plt
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorksDW' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
sql = "SELECT DATEDIFF(year, c.BirthDate, GETDATE()) AS Age FROM [dbo].[FactInternetSales] s INNER JOIN dbo.DimCustomer c ON s.CustomerKey = c.CustomerKey"
df = pd.read_sql(sql, cnxn)
df.hist(bins=10)
```

이 표시에서는 FactInternetSales 테이블에 있는 고객의 연령 분포를 보여 줍니다.

![Pandas 히스토그램](./media/python-histogram.png)