---
title: "SQL Server 및 Azure SQL Database에서 데이터 가져오기 및 내보내기 | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 3c41be0642b13b63367c5601b716b506808472e7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/14/2017

---
# <a name="import-and-export-data-from-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 데이터 가져오기 및 내보내기
다양한 메서드를 사용하여 SQL Server 및 Azure SQL Database에서 데이터를 가져오고 내보낼 수 있습니다. 이러한 메서드는 Transact-SQL 문, 명령줄 도구 및 마법사를 포함합니다.

다양한 데이터 형식에서 데이터를 가져오고 내보낼 수도 있습니다. 이러한 형식은 플랫 파일, Excel, 주요 관계형 데이터베이스 및 다양한 클라우드 서비스를 포함합니다.

## <a name="methods-for-importing-and-exporting-data"></a>데이터 가져오기 및 내보내기 방법

### <a name="use-transact-sql-statements"></a>Transact-SQL 문 사용
`BULK INSERT` 또는 `OPENROWSET(BULK...)` 명령을 사용하여 데이터를 가져올 수 있습니다. 일반적으로 SSMS(SQL Server Management Studio)에서 이러한 명령을 실행합니다. 자세한 내용은 [BULK INSERT 또는 OPENROWSET(BULK...)을 사용하여 데이터 대량 가져오기](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)를 참조하세요.

### <a name="use-bcp-from-the-command-prompt"></a>명령 프롬프트에서 BCP 사용
BCP 명령줄 유틸리티를 사용하여 데이터를 가져오고 내보낼 수 있습니다. 자세한 내용은 [bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)를 참조하세요.

### <a name="use-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사 사용
SQL Server 가져오기 및 내보내기 마법사를 사용하여 다양한 원본 및 대상 간에 데이터를 가져오고 내보낼 수 있습니다. 마법사를 사용하려면 SSIS(SQL Server Integration Services) 또는 SSDT(SQL Server Data Tools)가 설치되어 있어야 합니다. 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

### <a name="design-your-own-import-or-export"></a>사용자 고유 가져오기 또는 내보내기 디자인
사용자 지정 데이터 가져오기를 디자인하려는 경우 다음 기능 또는 서비스 중 하나를 사용할 수 있습니다.
-   SQL Server Integration Services. 자세한 내용은 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)를 참조하세요.
-   Azure Data Factory. 자세한 내용은 [Azure Data Factory 소개](https://docs.microsoft.com/azure/data-factory/data-factory-introduction)를 참조하세요.

## <a name="data-formats-for-import-and-export"></a>가져오기 및 내보내기에 대한 데이터 형식

### <a name="supported-formats"></a>지원되는 형식

플랫 파일 또는 다양한 다른 파일 형식, 관계형 데이터베이스 및 클라우드 서비스 간에 데이터를 가져오고 내보낼 수 있습니다. 특정 도구에 대한 이러한 옵션에 대한 자세한 내용은 다음 항목을 참조하세요.
-   SQL Server 가져오기 및 내보내기 마법사의 경우 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)을 참조하세요.
-   SQL Server Integration Services의 경우 [Integration Services(SSIS) 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.
-   Azure Data Factory의 경우 [Azure Data Factory 커넥터](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-amazon-redshift-connector)를 참조하세요.

### <a name="commonly-used-data-formats"></a>일반적으로 사용되는 데이터 형식

일부 일반적으로 사용되는 데이터 형식에 대해 사용할 수 있는 특별 고려 사항 및 예제가 있습니다. 이러한 데이터 형식에 대해 자세히 알아보려면 다음 항목을 참조하세요.
-   Excel의 경우 [Excel에서 가져오기](import-data-from-excel-to-sql.md)를 참조하세요.
-   JSON의 경우 [JSON 문서 가져오기](../json/import-json-documents-into-sql-server.md)를 참조하세요.
-   XML의 경우 [XML 문서 가져오기 및 내보내기](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)를 참조하세요.
-   Azure Blob Storage의 경우 [Azure Blob Storage에서 가져오기 및 내보내기](examples-of-bulk-access-to-data-in-azure-blob-storage.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
가져오기 또는 내보내기 작업을 시작할 위치를 잘 모를 경우 SQL Server 가져오기 및 내보내기 마법사를 사용하세요. 빠른 소개의 경우 [가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)을 참조하세요.

