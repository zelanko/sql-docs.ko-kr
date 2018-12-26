---
title: DQS 데이터베이스 분리 및 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 50c29f343399e0cc7d3c65d630ac622278d10eec
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032020"
---
# <a name="detaching-and-attaching-dqs-databases"></a>DQS 데이터베이스 분리 및 연결
  이 항목에서는 DQS 데이터베이스를 분리 및 연결하는 방법에 대해 설명합니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Limitations"></a> 제한 사항  
 제한 사항 목록은 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md)의 데이터베이스를 분리하는 방법에 대해 설명합니다.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   DQS에서 실행 중인 작업이나 프로세스가 없는지 확인합니다. 이는 **작업 모니터링** 화면을 사용하여 확인할 수 있습니다. 이 화면을 사용하는 방법은 [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md)을 참조하세요.  
  
-   [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에 로그온한 사용자가 없는지 확인합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
-   DQS 데이터베이스를 분리하려면 Windows 사용자 계정은 SQL Server 인스턴스에서 db_owner 고정 서버 역할의 멤버여야 합니다.  
  
-   데이터베이스를 연결하려면 Windows 사용자 계정에 CREATE DATABASE, CREATE ANY DATABASE 또는 ALTER ANY DATABASE 권한이 있어야 합니다.  
  
-   DQS에서 실행 중인 작업을 종료하거나 실행 중인 프로세스를 중지하려면 DQS_MAIN 데이터베이스에 대한 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Detach"></a> DQS 데이터베이스 분리  
 SQL Server Management Studio를 사용하여 DQS 데이터베이스를 분리하는 경우 분리된 파일은 컴퓨터에 남아 있으므로 동일한 SQL Server 인스턴스에 다시 연결되거나 다른 서버로 이동하여 거기에서 연결될 수 있습니다. DQS 데이터베이스 파일은 대개 Data Quality Services 컴퓨터의 다음 위치: C:\Program Files\Microsoft SQL Server\MSSQL12. *< Instance_Name >* \MSSQL\DATA 합니다.  
  
1.  Microsoft SQL Server Management Studio를 시작하고 적합한 SQL Server 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 **데이터베이스** 노드를 확장합니다.  
  
3.  **DQS_MAIN** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **분리**를 클릭합니다. **데이터베이스 분리** 대화 상자가 나타납니다.  
  
4.  **삭제** 열 아래 확인란을 선택하고 **확인** 을 클릭하여 DQS_MAIN 데이터베이스를 분리합니다.  
  
5.  DQS_PROJECTS 및 DQS_STAGING_DATA 데이터베이스에서 3단계와 4단계를 반복하여 해당 데이터베이스를 분리합니다.  
  
 Transact-SQL 문에서 sp_detach_db 저장 프로시저를 사용하여 DQS 데이터베이스를 분리할 수도 있습니다. Transact-SQL 문을 사용하여 데이터베이스를 분리하는 방법은 [Using Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) 의 [Detach a Database](../relational-databases/databases/detach-a-database.md)을 참조하세요.  
  
##  <a name="Attach"></a> DQS 데이터베이스 연결  
 다음 지침을 사용하여 DQS 데이터베이스를 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 가 설치된 다른 SQL Server 인스턴스에 연결하거나 분리되었던 SQL Server 인스턴스에 연결할 수 있습니다.  
  
1.  Microsoft SQL Server Management Studio를 시작하고 적합한 SQL Server 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **연결**을 클릭합니다. **데이터베이스 연결** 대화 상자가 나타납니다.  
  
3.  연결할 데이터베이스를 지정하려면 **추가**를 클릭합니다. **데이터베이스 파일 찾기** 대화 상자가 나타납니다.  
  
4.  데이터베이스가 있는 디스크 드라이브를 선택하고 디렉터리 트리를 확장하여 데이터베이스의 .mdf 파일을 찾은 다음 이 파일을 선택합니다. 예를 들어 DQS_MAIN 데이터베이스의 경우 다음 파일을 선택합니다.  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  **데이터베이스 정보** (아래쪽) 창에 연결될 파일 이름이 표시됩니다. 파일의 경로 이름을 확인하거나 변경하려면 **찾아보기** 단추(…)를 클릭합니다.  
  
6.  **확인** 을 클릭하여 DQS_MAIN 데이터베이스를 연결합니다.  
  
7.  DQS_PROJECTS 및 DQS_STAGING_DATA 데이터베이스에서 2~6단계를 반복하여 해당 데이터베이스를 연결합니다.  
  
8.  또한 DQS_MAIN 데이터베이스를 복원한 후 다음 단계에서 Transact-SQL 문을 실행해야 합니다. 그렇지 않으면 Data Quality 클라이언트 애플리케이션을 사용하여 Data Quality Server에 연결할 때 오류 메시지가 표시되고 연결할 수 없습니다. 하지만 DQS_PROJECTS 또는 DQS_STAGING_DATA 데이터베이스만 연결하고 DQS_MAIN은 연결하지 않은 경우에는 9단계와 10단계를 수행할 필요가 없습니다.  
  
     Transact-SQL 문을 실행하려면 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.  
  
9. 쿼리 편집기 창에서 다음 SQL 문을 복사합니다.  
  
    ```  
    ALTER DATABASE [DQS_MAIN] SET TRUSTWORTHY ON;  
    EXEC sp_configure 'clr enabled', 1;  
    RECONFIGURE WITH OVERRIDE  
    ALTER DATABASE [DQS_MAIN] SET ENABLE_BROKER  
    ALTER AUTHORIZATION ON DATABASE::[DQS_MAIN] TO [##MS_dqs_db_owner_login##]  
    ALTER AUTHORIZATION ON DATABASE::[DQS_PROJECTS] TO [##MS_dqs_db_owner_login##]  
  
    ```  
  
10. F5 키를 눌러 문을 실행합니다. 결과 창에서 문이 성공적으로 실행되었는지 확인합니다. 다음 메시지가 표시됩니다. `Configuration option 'clr enabled' changed from 1 to 1. Run the RECONFIGURE statement to install.`  
  
11. 연결할 수 있는지 확인하기 위해 Data Quality 클라이언트를 사용하여 Data Quality Server에 연결해 봅니다.  
  
 Transact-SQL 문을 사용하여 DQS 데이터베이스를 연결할 수도 있습니다. Transact-SQL 문을 사용하여 데이터베이스를 연결하는 방법은 [Using Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) 의 [Attach a Database](../relational-databases/databases/attach-a-database.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [DQS 데이터베이스 관리](../../2014/data-quality-services/manage-dqs-databases.md)  
  
  
