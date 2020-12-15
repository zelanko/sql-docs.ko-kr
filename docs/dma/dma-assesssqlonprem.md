---
title: SQL Server 마이그레이션 평가 수행
titleSuffix: Data Migration Assistant
description: Data Migration Assistant를 사용 하 여 다른 SQL Server 마이그레이션하기 전에 온-프레미스 SQL Server를 평가 하는 방법을 알아보고 Azure SQL Database
ms.date: 01/15/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: c88a289e21e7cd70980763474e82b7dd6cbd49c2
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489520"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Data Migration Assistant를 사용하여 SQL Server 마이그레이션 평가 수행

다음 단계별 지침은 온-프레미스 SQL Server로 마이그레이션하기 위한 첫 번째 평가, Azure VM에서 실행 되는 SQL Server 또는 Data Migration Assistant를 사용 하 여 Azure SQL Database를 수행 하는 데 도움이 됩니다.

   > [!NOTE]
   > Data Migration Assistant v 5.0에서는 응용 프로그램 코드에서 데이터베이스 연결 및 포함 된 SQL 쿼리를 분석 하는 기능이 도입 되었습니다. 자세한 내용은 [Data Migration Assistant를 사용 하 여 응용 프로그램의 데이터 액세스 계층을 평가 하](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430)는 블로그 게시물을 참조 하세요.

## <a name="create-an-assessment"></a>평가 만들기

1. **새로 만들기** (+) 아이콘을 선택 하 고 **평가** 프로젝트 형식을 선택 합니다.

2. 원본 및 대상 서버 유형을 설정합니다.

    온-프레미스 SQL Server 인스턴스를 최신 온-프레미스 SQL Server 인스턴스로 업그레이드 하는 경우 또는 Azure VM에서 호스트 되는 SQL Server 원본 및 대상 서버 유형을 **SQL Server** 로 설정 합니다. Azure SQL Database로 마이그레이션하는 경우 대신 대상 서버 유형을 **Azure SQL Database** 로 설정 합니다.

3. **만들기** 를 클릭합니다.

   ![평가 만들기](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>평가 옵션 선택

1. 마이그레이션하려는 대상 SQL Server 버전을 선택 합니다.

2. 보고서 유형을 선택 합니다.

   온-프레미스 SQL Server 또는 Azure VM 대상에서 호스트 되는 SQL Server으로 마이그레이션하기 위해 원본 SQL Server 인스턴스를 평가 하는 경우 다음 평가 보고서 유형 중 하나 또는 둘 다를 선택할 수 있습니다.

    - **호환성 문제**
    - **새 기능 권장 사항**

   ![SQL Server 대상에 대 한 평가 보고서 유형을 선택 합니다.](../dma/media/dma-assesssqlonprem/assessment-types.png)

   Azure SQL Database으로 마이그레이션하기 위해 원본 SQL Server 인스턴스를 평가 하는 경우 다음 평가 보고서 유형 중 하나 또는 둘 다를 선택할 수 있습니다.

    - **데이터베이스 호환성 확인**
    - **기능 패리티 확인**

    ![SQL Database 대상에 대 한 평가 보고서 유형 선택](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>평가할 데이터베이스 및 확장 이벤트 추적 추가

1. **원본 추가** 를 선택 하 여 연결 플라이 아웃 메뉴를 엽니다.

2. SQL server 인스턴스 이름을 입력 하 고 인증 유형을 선택한 다음 올바른 연결 속성을 설정 하 고 **연결** 을 선택 합니다.

3. 평가할 데이터베이스를 선택 하 고 **추가** 를 선택 합니다.

    > [!NOTE]
    > Shift 또는 Ctrl 키를 누른 채 **원본 제거** 를 클릭 하 여 여러 데이터베이스를 선택 하 여 제거할 수 있습니다. **원본 추가** 를 선택 하 여 여러 SQL Server 인스턴스에서 데이터베이스를 추가할 수도 있습니다.

4. 임시 또는 동적 SQL 쿼리나 응용 프로그램 데이터 계층을 통해 시작 된 DML 문이 있는 경우 원본 SQL Server에 대 한 작업을 캡처하기 위해 수집한 모든 확장 이벤트 세션 파일을 저장 한 폴더의 경로를 입력 합니다.

     다음 예에서는 응용 프로그램 데이터 계층 워크 로드를 캡처하기 위해 소스 SQL Server에 확장 이벤트 세션을 만드는 방법을 보여 줍니다.  최고 워크 로드를 나타내는 기간에 대 한 워크 로드를 캡처합니다.

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_batch_completed( 
        ACTION (sqlserver.sql_text,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_id))
    ADD TARGET package0.asynchronous_file_target(SET filename=N'C:\temp\Demos\DataLayerAppassess\DatalayerSession.xel')  
    WITH (MAX_MEMORY=2048 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=3 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
    go
    ---Start the session
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = START;
    ---Wait for few minutes
    
    ---Query events
        
        SELECT 
        object_name,
        CAST(event_data as xml) as event_data,
        file_name, 
        file_offset
    FROM sys.fn_xe_file_target_read_file('C:\temp\Demos\DataLayerAppassess\DatalayerSession*xel', 
                'C:\\temp\\Demos\\DataLayerAppassess\\DatalayerSession*xem', 
                null,
                null)
    ---Stop the session after capturing the peak load.
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = STOP;
        
        go
    ```

5. **다음** 을 클릭하여 평가를 시작합니다.

    ![원본 추가 및 평가 시작](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> 여러 평가를 동시에 실행하고 **모든 평가** 페이지를 열어서 평가 상태를 볼 수 있습니다.

## <a name="view-results"></a>결과 보기

평가 기간은 추가 된 데이터베이스 수와 각 데이터베이스의 스키마 크기에 따라 달라 집니다. 각 데이터베이스를 사용할 수 있게 되는 즉시 결과를 표시 합니다.

1. 평가를 완료 한 데이터베이스를 선택한 다음, 전환기를 사용 하 여 **호환성 문제** 및 **기능 권장 사항** 간을 전환 합니다.

2. **옵션** 페이지에서 선택한 대상 SQL Server 버전에서 지 원하는 모든 호환성 수준에서 호환성 문제를 검토 합니다.

영향을 받는 개체, 세부 정보 및 **주요 변경 내용**, **동작 변경 내용** 및 **더 이상 사용 되지 않는 기능** 에서 식별 된 모든 문제에 대 한 픽스를 분석 하 여 호환성 문제를 검토할 수 있습니다.

![평가 결과 보기](../dma/media/dma-assesssqlonprem/review-results.png)

마찬가지로 **성능**, **저장소** 및 **보안** 영역에 대해 기능 권장 사항을 검토할 수 있습니다.

기능 권장 사항에는 In-Memory OLTP, Columnstore, Stretch Database, Always Encrypted, 동적 데이터 마스킹, 투명한 데이터 암호화 등의 여러 가지 기능이 포함 됩니다.

![기능 권장 사항 보기](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

Azure SQL Database의 경우 평가는 마이그레이션 차단 문제와 기능 패리티 문제를 제공 합니다. 특정 옵션을 선택 하 여 두 범주에 대 한 결과를 검토 합니다.

- **SQL Server 기능 패리티** 범주는 포괄적인 권장 사항 집합, Azure에서 사용할 수 있는 대체 방법 및 완화 단계를 제공 합니다. 이를 통해 마이그레이션 프로젝트에서 이러한 작업을 계획할 수 있습니다.

  ![SQL Server 기능 패리티 정보 보기](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- **호환성 문제** 범주는 온-프레미스 SQL Server 데이터베이스를 Azure SQL 데이터베이스로 마이그레이션하는 것을 차단 하는 부분적으로 지원 되거나 지원 되지 않는 기능을 제공 합니다. 그런 다음 해당 문제를 해결 하는 데 도움이 되는 권장 사항을 제공 합니다.

  ![호환성 문제 보기](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>대상 준비를 위한 데이터 공간 평가

이러한 평가를 전체 데이터 공간으로 확장 하 고 Azure SQL Database로 마이그레이션할 SQL Server 인스턴스와 데이터베이스의 상대적 준비 상태를 확인 하려면 **Azure Migrate에 업로드** 를 선택 하 여 Azure Migrate 허브에 결과를 업로드 합니다.

이렇게 하면 Azure Migrate 허브 프로젝트에서 통합 결과를 볼 수 있습니다.

자세한 내용은 [여기](./dma-assess-sql-data-estate-to-sqldb.md)에서 목표 준비 평가에 대 한 단계별 지침을 제공 합니다.

   ![Azure Migrate에 결과 업로드](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>결과 내보내기

모든 데이터베이스가 평가를 완료 한 후 **보고서 내보내기** 를 선택 하 여 결과를 JSON 파일이 나 CSV 파일로 내보냅니다. 그런 다음 사용자의 편의를 위해 데이터를 분석할 수 있습니다.

## <a name="save-and-load-assessments"></a>평가 저장 및 로드

평가 결과를 내보낼 뿐만 아니라 파일에 평가 세부 정보를 저장 하 고 나중에 검토할 수 있도록 평가 파일을 로드할 수 있습니다.  자세한 내용은 [Data Migration Assistant를 사용 하 여 평가 저장 및 로드](../dma/dma-save-load-assessments.md)문서를 참조 하세요.
