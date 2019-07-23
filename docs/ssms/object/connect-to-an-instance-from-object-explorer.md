---
title: SQL Server 또는 Azure SQL Database에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aeb46551b33f40ba6c42de705559e20d8c7b0315
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264611"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>SQL Server 또는 Azure SQL Database에 연결

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
서버 및 데이터베이스를 사용하려면 먼저 서버에 연결해야 합니다. 여러 서버에 동시에 연결할 수 있습니다.

[SSMS(SQL Server Management Studio)](../download-sql-server-management-studio-ssms.md)는 여러 유형의 연결을 지원합니다. 이 문서에서는 SQL Server 및 Azure SQL Database에 연결(SQL Azure 단일 데이터베이스 또는 탄력적 풀)에 대한 세부 정보를 제공합니다. 다른 연결 옵션에 대한 내용은 이 페이지 하단의 [링크](#see-also)를 참조하세요.
  
## <a name="connecting-to-a-server"></a>Server에 연결  

1. **개체 탐색기**에서 **연결 > 데이터베이스 엔진...** 을 클릭합니다.

   ![connect](../media/connect-to-server/connect-db-engine.png)

1. **서버에 연결** 양식을 입력하고 **연결**을 클릭합니다.

   ![서버에 연결](../media/connect-to-server/connect.png)

1. Azure SQL Server에 연결하는 경우 방화벽 규칙을 만들려면 로그인하라는 메시지가 표시될 수 있습니다. **로그인...** (그렇지 않은 경우 아래 6단계로 건너뜀)을 클릭합니다.

   ![방화벽](../media/connect-to-server/firewall-rule-sign-in.png)

1. 성공적으로 로그인하면 특정 IP 주소로 양식이 미리 채워져 있습니다. IP 주소를 자주 변경하는 경우 범위에 액세스 권한을 쉽게 부여할 수 있으므로 환경에 가장 적합한 옵션을 선택합니다. 

   ![방화벽](../media/connect-to-server/new-firewall-rule.png)

1. 방화벽 규칙을 만들고 서버에 연결하려면 **확인**을 클릭합니다.

1. 성공적으로 연결되면 서버가 **개체 탐색기**에 표시됩니다.

   ![연결됨](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>Next Steps

[테이블 디자인, 생성 및 업데이트](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>참고 항목

[SSMS(SQL Server Management Studio)](../sql-server-management-studio-ssms.md)  
[SSMS(SQL Server Management Studio) 다운로드](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Azure Storage](../f1-help/connect-to-microsoft-azure-storage.md)  
