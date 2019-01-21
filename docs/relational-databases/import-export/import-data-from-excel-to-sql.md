---
title: Excel에서 SQL로 데이터 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77acf33ae4cdc4626f5467f136d8fb96b5ba96ed
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299553"
---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>Excel에서 SQL Server 또는 Azure SQL Database로 데이터 가져오기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [SQL Docs 목차에 대한 피드백을 공유하세요!](https://aka.ms/sqldocsurvey)

Excel 파일에서 SQL Server 또는 Azure SQL Database로 데이터를 가져오는 여러 가지 방법이 있습니다. 일부 방법을 사용하면 한 단계만 거쳐 Excel 파일에서 직접 데이터를 가져올 수 있습니다. 다른 방법을 사용하려면 가져오기 전에 Excel 데이터를 텍스트로 내보내야 합니다. 이 문서에서는 자주 사용하는 방법을 요약하고 자세한 정보의 링크를 제공합니다.

## <a name="list-of-methods"></a>메서드 목록

-   다음 도구 중 하나를 사용하여 Excel에서 SQL로 직접 한 단계만 거쳐 데이터를 가져올 수 있습니다.
    -   [SQL Server 가져오기 및 내보내기 마법사](#wiz)
    -   [SSIS(SQL Server Integration Services)](#ssis)
    -   [OPENROWSET](#openrowset) 함수
-   텍스트 파일을 가져오기 위해 Excel의 데이터를 텍스트로 내보내고 다음 도구 중 하나를 사용하여 두 단계를 거쳐 데이터를 가져올 수 있습니다.
    -   [플랫 파일 가져오기 마법사](#import-wiz)
    -   [BULK INSERT](#bulk-insert) 문
    -   [BCP](#bcp)
    -   [복사 마법사(Azure Data Factory)](#adf-wiz)
    -   [Azure Data Factory](#adf)

Excel 통합 문서에서 여러 워크시트를 가져오려는 경우 일반적으로 각 시트에서 한 번씩 이러한 도구를 각각 실행해야 합니다.

SSIS 또는 Azure Data Factory와 같은 복잡한 도구 및 서비스에 대한 자세한 설명은 이 목록의 범위에 포함되지 않습니다. 관심 있는 솔루션에 대한 자세한 내용을 알아보려면 제공된 링크로 이동하세요.

> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../../integration-services/load-data-to-from-excel-with-ssis.md)를 참조하세요.

## <a name="wiz"></a> SQL Server 가져오기 및 내보내기 마법사

SQL Server 가져오기 및 내보내기 마법사의 페이지를 단계별로 실행하여 Excel 파일에서 직접 데이터를 가져옵니다. 필요에 따라 설정을 SSIS(SQL Server Integration Services) 패키지로 저장하여 나중에 사용자 지정하고 다시 사용할 수 있습니다.

마법사를 시작하는 방법을 알아보려면 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.

Excel에서 SQL Server로 가져오기 위해 마법사를 사용한 예제를 보려면 [가져오기 및 내보내기 마법사의 이 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)을 참조하세요.

![Excel 데이터 원본에 연결](media/excel-connection.png)

## <a name="ssis"></a> SSIS(SQL Server Integration Services)

SSIS에 익숙하여 SQL Server 가져오기 및 내보내기 마법사가 실행되지 않게 하려면 Excel 원본 및 데이터 흐름에서 SQL Server 대상을 사용하는 SSIS 패키지를 만듭니다.

이러한 SSIS 구성 요소에 대한 자세한 내용은 다음 항목을 참조하세요.
-   [Excel 원본](../../integration-services/data-flow/excel-source.md)
-   [SQL Server 대상](../../integration-services/data-flow/sql-server-destination.md)

SSIS 패키지를 작성하는 방법을 알아보려면 [ETL 패키지를 만드는 방법](../../integration-services/ssis-how-to-create-an-etl-package.md) 자습서를 참조하세요.

![데이터 흐름의 구성 요소](media/excel-to-sql-data-flow.png)

## <a name="openrowset"></a>OPENROWSET 및 연결된 서버

> [!NOTE]
> Azure에서는 OPENROWSET 및 OPENDATASOURCE 함수가 SQL Database Managed Instance에서만 지원됩니다.

> [!NOTE]
> Excel 데이터 원본에 연결하는 ACE 공급자(이전의 Jet 공급자)는 대화형 클라이언트 쪽 사용을 위한 것입니다. 자동화 프로세스 또는 병렬로 실행되는 프로세스에서 특히 서버의 ACE 공급자를 사용하는 경우 예기치 않은 결과가 발생할 수 있습니다.

### <a name="distributed-queries"></a>분산 쿼리

Transact-SQL `OPENROWSET` 또는 `OPENDATASOURCE` 기능을 사용하여 Excel 파일에서 데이터를 직접 가져옵니다. 이 사용법을 *분산 쿼리*라고 합니다.

분산 커리를 실행하려면 다음 예제에 나온 것과 같이 먼저 `ad hoc distributed queries` 서버 구성 옵션을 사용하도록 설정해야 합니다. 자세한 내용은 [임시 분산 쿼리 서버 구성 옵션](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)을 참조하세요.

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

다음 코드 샘플은 `OPENROWSET`을 사용하여 Excel `Data` 워크시트의 데이터를 새 데이터베이스 테이블로 가져옵니다.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=D:\Desktop\Data.xlsx', [Data$]);
GO
```

다음은 `OPENDATASOURCE`와 같은 예제입니다.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=D:\Desktop\Data.xlsx;Extended Properties=Excel 12.0')...[Data$];
GO
```

가져온 데이터를 새 테이블을 만들지 않고 *기존* 테이블에 *추가*하려면 앞의 예제에서 사용된 `SELECT ... INTO ... FROM ...` 구문 대신에 `INSERT INTO ... SELECT ... FROM ...` 구문을 사용합니다.

Excel 데이터를 가져오지 않고 쿼리를 사용하려면 표준 `SELECT ... FROM ...` 구문을 사용하면 됩니다.

분산 쿼리에 대한 자세한 내용은 다음 항목을 참조하세요.
-   [분산 쿼리](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx) (분산 쿼리는 SQL Server 2016에서 계속 지원되지만 이 기능에 대한 설명서는 업데이트되지 않았습니다.)
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>연결된 서버

Excel 파일을 *연결된 서버*로 영구 연결을 구성할 수도 있습니다. 다음 예제에서는 기존의 Excel 연결된 서버 `EXCELLINK`에 있는 `Data` 워크시트에서 `Data_ls`라는 새 데이터베이스 테이블로 데이터를 가져옵니다.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

다음 예제에 나온 것과 같이 SQL Server Management Studio에서 연결된 서버 또는 시스템 저장 프로시저 `sp_addlinkedserver`를 실행하여 연결된 서버를 만들 수 있습니다.

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'D:\Desktop\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

연결된 서버에 대한 자세한 내용은 다음 항목을 참조하세요.
-   [연결된 서버 만들기](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

연결된 서버 및 분산 쿼리 모두에 대한 정보 및 예제는 다음 항목을 참조하세요.
-   [SQL Server 연결된 서버 및 분산 쿼리와 함께 Excel을 사용하는 방법](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
-   [Excel에서 SQL Server로 데이터를 가져오는 방법](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prereq"></a> 필수 구성 요소 - Excel 데이터를 텍스트로 저장
이 페이지에 설명된 나머지 방법(BULK INSERT 문, BCP 도구 또는 Azure Data Factory 등)을 사용하려면 먼저 Excel 데이터를 텍스트 파일로 내보내야 합니다.

Excel에서 **파일 | 다른 이름으로 저장**을 선택한 다음, **텍스트(탭으로 구분)(\*.txt)** 또는 **CSV(쉼표로 구분)(\*.csv)** 를 대상 파일 형식으로 선택합니다.

통합 문서에서 여러 워크시트를 가져오려는 경우 각 시트를 선택한 다음, 이 프로시저를 반복합니다. **다른 이름으로 저장** 명령은 활성 시트만을 내보냅니다.

> [!TIP]
> 데이터 가져오기 도구로 최상의 결과를 얻으려면, 데이터의 열 헤더 및 행만 포함하는 시트를 저장합니다. 저장된 데이터에 페이지 제목, 빈 줄, 메모 등이 포함되어 있는 경우 나중에 데이터를 가져올 때 예기치 않은 결과가 발생할 수 있습니다.

## <a name="import-wiz"></a>플랫 파일 가져오기 마법사

플랫 파일 가져오기 마법사 페이지를 단계별로 실행하여 텍스트 파일로 저장된 데이터를 가져옵니다.

앞의 [필수 구성 요소](#prereq) 섹션에서 설명한 대로 플랫 파일 가져오기 마법사를 사용하여 가져오기 전에 Excel 데이터를 텍스트로 내보내야 합니다.

플랫 파일 가져오기 마법사에 대한 자세한 내용은 [SQL 마법사로 플랫 파일 가져오기](import-flat-file-wizard.md)를 참조하세요.

## <a name="bulk-insert"></a> BULK INSERT 명령

`BULK INSERT`는 SQL Server Management Studio에서 실행할 수 있는 Transact-SQL 명령입니다. 다음 예제에서는 `Data.csv` 쉼표로 구분된 파일에서 기존 데이터베이스 테이블로 데이터를 로드합니다.

앞의 [필수 구성 요소](#prereq) 섹션에서 설명한 대로 BULK INSERT를 사용하여 데이터를 가져오려면 먼저 Excel 데이터를 텍스트로 내보내야 합니다. BULK INSERT는 Excel 파일을 직접 읽을 수 없습니다.

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'D:\Desktop\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

자세한 내용은 다음 항목을 참조하세요.
-   [BULK INSERT 또는 OPENROWSET(BULK...)을 사용하여 데이터 대량 가져오기](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp"></a> BCP 도구

BCP는 명령 프롬프트에서 실행되는 프로그램입니다. 다음 예제에서는 `Data.csv` 쉼표로 구분된 파일에서 기존 `Data_bcp` 데이터베이스 테이블로 데이터를 로드합니다.

앞의 [필수 구성 요소](#prereq) 섹션에서 설명한 대로 BCP를 사용하여 데이터를 가져오려면 먼저 Excel 데이터를 텍스트로 내보내야 합니다. BCP는 직접 Excel 파일을 읽을 수 없습니다.

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

BCP에 대한 자세한 내용은 다음 항목을 참조하세요.
-   [bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [bcp 유틸리티](../../tools/bcp-utility.md)
-   [대량 내보내기 또는 가져오기를 위한 데이터 준비](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="adf-wiz"></a> 복사 마법사(Azure Data Factory)
Azure Data Factory 복사 마법사 페이지를 단계별로 실행하여 텍스트 파일로 저장된 데이터를 가져옵니다.

앞의 [필수 구성 요소](#prereq) 섹션에서 설명한 대로 Azure Data Factory를 사용하여 데이터를 가져오려면 먼저 Excel 데이터를 텍스트로 내보내야 합니다. Data Factory는 직접 Excel 파일을 읽을 수 없습니다.

복사 마법사에 대한 자세한 내용은 다음 항목을 참조하세요.
-   [데이터 팩터리 복사 마법사](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [자습서: 데이터 팩터리 복사 마법사를 사용하여 복사 활동으로 파이프라인을 만듭니다](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial).

## <a name="adf"></a> Azure Data Factory
Azure Data Factory에 익숙하여 복사 마법사를 실행되지 않게 하려면 텍스트 파일을 SQL Server 또는 Azure SQL Database로 복사하는 복사 작업으로 파이프라인을 만듭니다.

앞의 [필수 구성 요소](#prereq) 섹션에서 설명한 대로 Azure Data Factory를 사용하여 데이터를 가져오려면 먼저 Excel 데이터를 텍스트로 내보내야 합니다. Data Factory는 직접 Excel 파일을 읽을 수 없습니다.

이러한 Data Factory 원본 및 싱크에 대한 자세한 내용은 다음 항목을 참조하세요.
-   [파일 시스템](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Azure SQL Database*](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

Azure Data Factory를 사용해 데이터를 복사하는 방법을 알아보려면 다음 항목을 참조하세요.
-   [복사 활동을 사용하여 데이터 이동](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [자습서: Azure Portal을 사용하여 복사 활동으로 파이프라인 만들기](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="see-also"></a>참고 항목
[SSIS(SQL Server Integration Services)를 사용하여 Excel에서 데이터 가져오기 또는 Excel로 데이터 내보내기](../../integration-services/load-data-to-from-excel-with-ssis.md)
