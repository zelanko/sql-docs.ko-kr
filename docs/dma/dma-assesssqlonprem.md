---
title: SQL Server 마이그레이션 평가 수행
titleSuffix: Data Migration Assistant
description: 다른 SQL Server 또는 Azure SQL Database로 마이그레이션하기 전에 데이터 마이그레이션 도우미를 사용하여 온-프레미스 SQL Server를 평가하는 방법을 알아봅니다.
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
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 59dc8c96ebda5ac66fb6701d480cb6d633e83158
ms.sourcegitcommit: 48e259549f65f0433031ed6087dbd5d9c0a51398
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80809745"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Data Migration Assistant를 사용하여 SQL Server 마이그레이션 평가 수행

다음 단계별 지침은 온-프레미스 SQL Server, Azure VM에서 실행되는 SQL Server 또는 데이터 마이그레이션 도우미를 사용하여 Azure SQL Database로 마이그레이션하기 위한 첫 번째 평가를 수행하는 데 도움이 됩니다.

   > [!NOTE]
   > 데이터 마이그레이션 도우미 v5.0응용 프로그램 코드에서 데이터베이스 연결 및 포함된 SQL 쿼리를 분석하기 위한 지원을 소개합니다. 자세한 내용은 블로그 게시물 [데이터 마이그레이션 도우미를 사용하여 응용 프로그램의 데이터 액세스 계층을 평가합니다.](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430)

## <a name="create-an-assessment"></a>평가 만들기

1. **새(+)** 아이콘을 선택한 다음 **평가** 프로젝트 유형을 선택합니다.

2. 원본 및 대상 서버 유형을 설정합니다.

    온-프레미스 SQL Server 인스턴스를 최신 온-프레미스 SQL Server 인스턴스 또는 Azure VM에서 호스팅되는 SQL Server로 업그레이드하는 경우 원본 및 대상 서버 유형을 **SQL Server로**설정합니다. Azure SQL Database로 마이그레이션하는 경우 대상 서버 유형을 **Azure SQL Database**로 설정합니다.

3. **만들기**를 클릭합니다.

   ![평가 만들기](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>평가 옵션 선택

1. 마이그레이션할 대상 SQL Server 버전을 선택합니다.

2. 보고서 유형을 선택합니다.

   온-프레미스 SQL Server 또는 Azure VM 대상에서 호스팅되는 SQL Server로 마이그레이션하기 위해 원본 SQL Server 인스턴스를 평가할 때 다음 평가 보고서 유형 중 하나 또는 둘 다를 선택할 수 있습니다.

    - **호환성 문제**
    - **새로운 기능의 권장 사항**

   ![SQL Server 대상에 대한 평가 보고서 유형 선택](../dma/media/dma-assesssqlonprem/assessment-types.png)

   Azure SQL Database로 마이그레이션하기 위해 원본 SQL Server 인스턴스를 평가할 때 다음 평가 보고서 유형 중 하나 또는 둘 다를 선택할 수 있습니다.

    - **데이터베이스 호환성 확인**
    - **기능 패리티 확인**

    ![SQL 데이터베이스 대상에 대한 평가 보고서 유형 선택](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>데이터베이스 및 확장 이벤트 추적을 추가하여 평가

1. 연결 플라이아웃 메뉴를 열려면 **소스 추가를** 선택합니다.

2. SQL Server 인스턴스 이름을 입력하고 인증 유형을 선택하고 올바른 연결 속성을 설정한 다음 **연결을**선택합니다.

3. 평가할 데이터베이스를 선택한 다음 **추가 를**선택합니다.

    > [!NOTE]
    > Shift 또는 Ctrl 키를 누를 때 선택한 다음 소스 **제거를**클릭하여 여러 데이터베이스를 제거할 수 있습니다. **소스 추가를**선택하여 여러 SQL Server 인스턴스의 데이터베이스를 추가할 수도 있습니다.

4. 임시 또는 동적 SQL 쿼리 또는 응용 프로그램 데이터 계층을 통해 시작된 DML 문이 있는 경우 원본 SQL Server에서 워크로드를 캡처하기 위해 수집한 모든 확장 이벤트 세션 파일을 배치한 폴더에 대한 경로를 입력합니다.

     다음 예제에서는 응용 프로그램 데이터 계층 워크로드를 캡처하기 위해 원본 SQL Server에서 확장 된 이벤트 세션을 만드는 방법을 보여 줍니다.  최대 워크로드를 나타내는 기간 동안 워크로드를 캡처합니다.

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

5. **다음**을 클릭하여 평가를 시작합니다.

    ![소스 추가 및 평가 시작](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> 여러 평가를 동시에 실행하고 **모든 평가** 페이지를 열어서 평가 상태를 볼 수 있습니다.

## <a name="view-results"></a>결과 보기

평가 기간은 추가된 데이터베이스 수와 각 데이터베이스의 스키마 크기에 따라 달라집니다. 결과는 사용 가능한 즉시 각 데이터베이스에 대해 표시됩니다.

1. 평가를 완료한 데이터베이스를 선택한 다음 스위처를 사용하여 **호환성 문제와** **기능 권장 사항** 간에 전환합니다.

2. **옵션** 페이지에서 선택한 대상 SQL Server 버전에서 지원하는 모든 호환성 수준에서 호환성 문제를 검토합니다.

영향을 받는 개체, 해당 세부 정보 및 **주요 변경**내용, **동작 변경**및 사용되지 않는 **기능에서 식별된**모든 문제에 대한 수정 프로그램을 분석하여 호환성 문제를 검토할 수 있습니다.

![평가 결과 보기](../dma/media/dma-assesssqlonprem/review-results.png)

마찬가지로 **성능,** **저장소**및 **보안** 영역에서 기능 권장 사항을 검토할 수 있습니다.

기능 권장 사항은 인메모리 OLTP, 컬럼스토어, 스트레치 데이터베이스, 항상 암호화된 동적 데이터 마스킹 및 투명 데이터 암호화와 같은 다양한 기능을 다룹니다.

![피처 권장 사항 보기](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

Azure SQL Database의 경우 평가는 마이그레이션 차단 문제 및 기능 패리티 문제를 제공합니다.특정 옵션을 선택하여 두 범주의 결과를 검토합니다.

- **SQL Server 기능 패리티** 범주는 포괄적인 권장 사항 집합, Azure에서 사용할 수 있는 대체 방법 및 완화 단계를 제공합니다. 마이그레이션 프로젝트에서 이러한 노력을 계획하는 데 도움이 됩니다.

  ![SQL Server 피처 패리티에 대한 정보 보기](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- **호환성 문제** 범주는 온-프레미스 SQL Server 데이터베이스에서 Azure SQL 데이터베이스로 마이그레이션하는 것을 차단하는 부분적으로 지원하거나 지원되지 않는 기능을 제공합니다.그런 다음 이러한 문제를 해결하는 데 도움이 되는 권장 사항을 제공합니다.

  ![호환성 문제 보기](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>대상 준비 상태를 위한 데이터 부동산 평가

이러한 평가를 전체 데이터 부동산으로 추가로 확장하고 Azure SQL Database로 마이그레이션하기 위한 SQL Server 인스턴스 및 데이터베이스의 상대적 준비 상태를 찾으려면 Azure 마이그레이션에 **대한 업로드를**선택하여 결과를 Azure 마이그레이션 허브에 업로드합니다.

이렇게 하면 Azure 마이그레이션 허브 프로젝트에서 통합된 결과를 볼 수 있습니다.

대상 준비 평가에 대한 자세한 단계별 지침은 [여기에서](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017)확인할 수 있습니다.

   ![Azure 마이그레이션에 결과 업로드](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>결과 내보내기

모든 데이터베이스가 평가를 완료한 후 **내보내기 보고서를** 선택하여 결과를 JSON 파일 또는 CSV 파일로 내보냅니다. 그런 다음 자신의 편의에 따라 데이터를 분석 할 수 있습니다.

## <a name="save-and-load-assessments"></a>평가 저장 및 로드

평가 결과를 내보내는 것 외에도 평가 세부 정보를 파일에 저장하고 나중에 검토할 수 있도록 평가 파일을 로드할 수 있습니다.  자세한 내용은 [데이터 마이그레이션 도우미를 사용하여 평가 저장 및 로드](../dma/dma-save-load-assessments.md)를 참조하세요.
