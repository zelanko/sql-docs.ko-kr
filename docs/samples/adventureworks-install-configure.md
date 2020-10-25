---
title: AdventureWorks 예제 데이터베이스
description: Transact-sql (T-sql), SQL Server Management Studio (SSMS) 또는 Azure Data Studio를 사용 하 여 SQL Server에 AdventureWorks 샘플 데이터베이스를 다운로드 하 고 설치 하려면 다음 지침을 따르세요.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/16/2020
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 1482104a0c8ffea7f7f2502b83b9b268b7bb08d2
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523960"
---
# <a name="adventureworks-sample-databases"></a>AdventureWorks 예제 데이터베이스
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 문서에서는 AdventureWorks 샘플 데이터베이스를 다운로드 하 고 SQL Server 및 Azure SQL Database으로 복원 하는 방법에 대 한 지침을 제공 하는 직접 링크를 제공 합니다. 

예제에 대 한 자세한 내용은 [샘플 GitHub 리포지토리](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases)를 참조 하세요. 

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019) 또는 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) 또는 [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)


## <a name="download-backup-files"></a>백업 파일 다운로드 

이러한 링크를 사용 하 여 시나리오에 적합 한 예제 데이터베이스를 다운로드 합니다. 

- **OLTP** 데이터는 가장 일반적인 온라인 트랜잭션 처리 워크 로드에 대 한 것입니다. 
- **DW (데이터 웨어하우스)** 데이터는 데이터 웨어하우징 작업에 대 한 데이터입니다. 
- **경량 (LT)** 데이터는 경량 및 pared down 버전의 **OLTP** 샘플입니다. 

필요한 것이 확실 하지 않은 경우 SQL Server 버전과 일치 하는 OLTP 버전으로 시작 합니다. 

|**OLTP** |**데이터 웨어하우스** |**간단한 기능**|
|---------|---------|---------|
|[AdventureWorks2019](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2019.bak)|[AdventureWorksDW2019](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2019.bak)|[AdventureWorksLT2019](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2019.bak)|
|[AdventureWorks2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)|[AdventureWorksDW2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)|[AdventureWorksLT2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2017.bak)|
|[AdventureWorks2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)|[AdventureWorksDW2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)|[AdventureWorksLT2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2016.bak)|
|[AdventureWorks2016_EXT .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016_EXT.bak)|[AdventureWorksDW2016_EXT .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016_EXT.bak)| N/A |
|[AdventureWorks2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)|[AdventureWorksDW2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)|[AdventureWorksLT2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2014.bak)|
|[AdventureWorks2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)|[AdventureWorksDW2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)|[AdventureWorksLT2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2012.bak)|
|[AdventureWorks2008R2](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)| [AdventureWorksDW2008R2](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak) | N/A |

GitHub에서 직접 추가 파일을 찾을 수 있습니다. 

- [SQL Server 2014-2019](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL Server 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL Server 2008 및 2008 R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)


## <a name="restore-to-sql-server"></a>SQL Server 복원 

이 파일을 사용 하 여 `.bak` 예제 데이터베이스를 SQL Server 인스턴스로 복원할 수 있습니다. [RESTORE (transact-sql)](../t-sql/statements/restore-statements-transact-sql.md) 명령을 사용 하거나 [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) 또는 [AZURE DATA STUDIO](../azure-data-studio/download-azure-data-studio.md)에서 그래픽 인터페이스 (GUI)를 사용 하 여이 작업을 수행할 수 있습니다.

# <a name="sql-server-management-studio-ssms"></a>[SSMS(SQL Server Management Studio)](#tab/ssms)

SSMS (SQL Server Management Studio)를 사용 하는 데 익숙하지 않은 경우 시작 하기 위해 [연결 & 쿼리](../ssms/quickstarts/connect-query-sql-server.md) 를 볼 수 있습니다. 

SQL Server Management Studio에서 데이터베이스를 복원 하려면 다음 단계를 수행 합니다.

1. `.bak` [백업 파일 다운로드](#download-backup-files) 섹션에 제공 된 링크 중 하나에서 적절 한 파일을 다운로드 합니다.
2. 파일을 `.bak` SQL Server 백업 위치로 이동 합니다. 이는 SQL Server의 설치 위치, 인스턴스 이름 및 버전에 따라 달라 집니다. 예를 들어 SQL Server 2019의 기본 인스턴스에 대 한 기본 위치는 다음과 같습니다.

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`. 

3. SSMS (SQL Server Management Studio)를 열고의 SQL Server에 연결 합니다. 
4. 데이터베이스 복원 개체 탐색기 **에서 데이터베이스를 마우스** 오른쪽 단추로 클릭 **Object Explorer**  >  **Restore Database...** 하 여 **데이터베이스 복원** 마법사를 시작 합니다. 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-ssms.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::


1. **장치** 를 선택 하 고 줄임표 **(...)** 를 선택 하 여 장치를 선택 합니다. 
1. **추가** 를 선택한 다음 `.bak` 최근에이 위치로 이동한 파일을 선택 합니다. 파일을이 위치로 이동 했지만 마법사에서 볼 수 없는 경우 일반적으로이 폴더에서이 파일에 대 한 사용 권한이 없는 SQL Server에 로그인 한 사용자에 게는 권한 문제가 SQL Server 표시 됩니다. 
1. **확인** 을 선택 하 여 데이터베이스 백업 선택을 확인 하 고 **백업 장치 선택** 창을 닫습니다. 
1. **파일** 탭을 확인 하 여 **데이터베이스 복원** 마법사에서 위치 및 파일 이름이 원하는 위치 및 파일 이름과 일치 하는지 **확인 합니다.** 
1. **확인**을 선택하여 데이터베이스를 복원합니다. 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-wizard-ssms.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::

SQL Server 데이터베이스 복원에 대 한 자세한 내용은 SSMS를 [사용 하 여 데이터베이스 백업 복원](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)을 참조 하세요.

# <a name="transact-sql-t-sql"></a>[Transact-sql (T-sql)](#tab/tsql)

Transact-sql (T-sql)을 사용 하 여 샘플 데이터베이스를 복원할 수 있습니다. AdventureWorks2019 복원에 대 한 예제는 아래에 제공 되지만 데이터베이스 이름과 설치 파일 경로는 사용자 환경에 따라 다를 수 있습니다. 

AdventureWorks2019를 복원 하려면 사용자 환경에 적절 한 값을 수정 하 고 다음 Transact-sql (T-sql) 명령을 실행 합니다.

```sql
USE [master]
RESTORE DATABASE [AdventureWorks2019] 
FROM  DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\AdventureWorks2019.bak' 
WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO

```

# <a name="azure-data-studio"></a>[Azure Data Studio](#tab/data-studio)

[Azure Data Studio Studio](../azure-data-studio/download-azure-data-studio.md)를 사용 하는 데 익숙하지 않은 경우 시작 하기 위한 [연결 & 쿼리](../azure-data-studio/quickstart-sql-server.md) 를 볼 수 있습니다.

Azure Data Studio에서 데이터베이스를 복원 하려면 다음 단계를 수행 합니다.

1. `.bak` [백업 파일 다운로드](#download-backup-files) 섹션에 제공 된 링크 중 하나에서 적절 한 파일을 다운로드 합니다.
1. 파일을 `.bak` SQL Server 백업 위치로 이동 합니다. 이는 SQL Server의 설치 위치, 인스턴스 이름 및 버전에 따라 달라 집니다. 예를 들어 SQL Server 2019의 기본 인스턴스에 대 한 기본 위치는 다음과 같습니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`.

1. Azure Data Studio Studio를 열고 SQL Server 인스턴스에 연결 합니다.
1. 서버를 마우스 오른쪽 단추로 클릭 하 고 **관리**를 선택 합니다.

   :::image type="content" source="media/adventureworks-install-configure/ads-manage.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::

1. **복원** 선택

   :::image type="content" source="media/adventureworks-install-configure/ads-restore-database.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::

1. **일반** 탭에서 **원본**아래에 나열 된 값을 입력 합니다.
    1. 다음 **에서 복원**에서 *백업 파일*을 선택 합니다.
    1. **백업 파일 경로**아래에서 .bak 파일을 저장 한 위치를 선택 합니다. 
    
   :::image type="content" source="media/adventureworks-install-configure/ads-source.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::
    
    그러면 **데이터베이스**, **대상 데이터베이스** 및 **복원과**같은 나머지 필드를 자동으로 채웁니다. 

   :::image type="content" source="media/adventureworks-install-configure/ads-destination-restore-plan.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::

1. **복원** 을 선택 하 여 데이터베이스를 복원 합니다. 

   :::image type="content" source="media/adventureworks-install-configure/ads-restore.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::

---

## <a name="deploy-to-azure-sql-database"></a>Azure SQL Database에 배포

샘플 Azure SQL Database 데이터를 볼 수 있는 두 가지 옵션이 있습니다. 새 데이터베이스를 만들 때 예제를 사용 하거나 SSMS (SQL Server Management Studio)를 사용 하 여 SQL Server에서 Azure로 직접 데이터베이스를 배포할 수 있습니다.

대신 Azure SQL Managed Instance에 대 한 샘플 데이터를 가져오려면 [wwpn을 sql Managed Instance으로 복원](/azure/azure-sql/managed-instance/restore-sample-database-quickstart)을 참조 하세요. 

### <a name="deploy-new-sample-database"></a>새 예제 데이터베이스 배포

Azure SQL Database에서 새 데이터베이스를 만들 때 빈 데이터베이스 또는 예제 데이터베이스를 만드는 옵션이 있습니다. 

예제 데이터베이스를 사용 하 여 새 데이터베이스를 만들려면 다음 단계를 수행 합니다. 

1. Azure Portal에 연결 합니다.
1. 탐색 창의 왼쪽 위에서 **리소스 만들기** 를 선택 합니다. 
1. **데이터베이스** 를 선택 하 고 **SQL Database**를 선택 합니다. 
1. 요청 된 정보를 입력 하 여 데이터베이스를 만듭니다. 
1. **추가 설정** 탭에서 **데이터 원본**아래의 기존 데이터로 **샘플** 을 선택 합니다. 

   :::image type="content" source="media/adventureworks-install-configure/deploy-sample-to-azure.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::

1. **만들기** 를 선택 하 여 AdventureWorksLT 데이터베이스의 복원 된 복사본 인 새 SQL Database를 만듭니다. 


### <a name="deploy-database-from-sql-server"></a>SQL Server에서 데이터베이스 배포

SQL Server Management Studio는 데이터베이스를 Azure SQL Database에 직접 배포 하는 기능을 제공 합니다. 이 메서드는 현재 데이터 유효성 검사를 제공 하지 않으므로 개발 및 테스트를 위한 것 이며 프로덕션에 사용 하면 안 됩니다. 

SQL Server에서 Azure SQL Database으로 예제 데이터베이스를 배포 하려면 다음 단계를 수행 합니다.

1. SQL Server Management Studio에서 SQL Server에 연결 합니다. 
1. 아직 수행 하지 않은 경우 [SQL Server에 샘플 데이터베이스를 복원](#restore-to-sql-server)합니다. 
1. **개체 탐색기**  >  **작업**  >  **Microsoft Azure SQL Database에 데이터베이스 배포**...를 클릭 하 여 복원 된 데이터베이스를 마우스 오른쪽 단추로 클릭 합니다. 

   :::image type="content" source="media/adventureworks-install-configure/deploy-db-to-azure.png" alt-text="개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 데이터베이스 복원을 선택 하 여 데이터베이스를 복원 하도록 선택 하는 방법을 보여 주는 스크린샷":::

1. 마법사에 따라 Azure SQL Database에 연결 하 고 데이터베이스를 배포 합니다. 


## <a name="creation-scripts"></a>작성 스크립트

데이터베이스를 복원 하는 대신 스크립트를 사용 하 여 버전에 관계 없이 AdventureWorks 데이터베이스를 만들 수 있습니다. 

아래 스크립트를 사용 하 여 전체 AdventureWorks 데이터베이스를 만들 수 있습니다. 

- [AdventureWorks OLTP 스크립트 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 스크립트 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

스크립트 사용에 대 한 추가 정보는 [GitHub](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)에서 찾을 수 있습니다. 

## <a name="next-steps"></a>다음 단계

예제 데이터베이스를 복원한 후에는 다음 자습서를 사용 하 여 SQL Server 시작 하세요. 


[SQL Server 데이터베이스 엔진에 대 한 자습서](../relational-databases/database-engine-tutorials.md)   
[SQL Server Management Studio 연결 및 쿼리 (SSMS)](../ssms/quickstarts/connect-query-sql-server.md)   
[Azure Data Studio 연결 및 쿼리](../ssms/quickstarts/connect-query-sql-server.md)