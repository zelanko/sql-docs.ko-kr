---
title: 데이터 요금-SQL 샘플 데이터베이스를 생성 하는 WideWorldImporters | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ace1f771ef3a77a6f7db0072442affe181d7872
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 데이터 생성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 및 WideWorldImportersDW 데이터베이스의 릴리스 버전에는 데이터베이스에서 생성 된 날짜까지 2013, 년 1 월 1 일에서 데이터가 있습니다.

이러한 예제 데이터베이스를 사용 하는 경우에 최신 샘플 데이터를 포함 하는 것이 좋습니다.

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters에서 데이터 생성

생성 하려면 현재 날짜 까지의 데이터 샘플:

1. 그렇게 하지 않은 경우에 WideWorldImporters 데이터베이스의 정리 버전이 설치 합니다. 설치 지침을 참조 하십시오. [설치 및 구성](wide-world-importers-oltp-install-configure.md)합니다.
2. 데이터베이스에 다음 문을 실행 합니다.

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    이 문은 현재 날짜 까지의 데이터베이스에 샘플 판매 및 구매 데이터를 추가합니다. 일별 데이터 생성의 진행 상태를 표시합니다. 데이터 생성에 대 한 데이터를 요구 하는 매년 약 10 분 정도 걸릴 수 있습니다. 데이터 생성에 사용 되는 임의 요인을, 때문에 실행 사이 생성 되는 데이터의 일부 차이점이 있습니다.

    하루에 한 주문에 대해 생성 된 데이터의 양을 늘리거나 설정, 매개 변수 값을 변경 `@AverageNumberOfCustomerOrdersPerDay`합니다. 매개 변수를 사용 하 여 `@SaturdayPercentageOfNormalWorkDay` 및 `@SundayPercentageOfNormalWorkDay` 주말에 대 한 주문 횟수를 확인 하려면.

## <a name="import-generated-data-in-wideworldimportersdw"></a>WideWorldImportersDW에 데이터를 생성 하는 가져오기

WideWorldImportersDW OLAP 데이터베이스의 현재 날짜 까지의 샘플 데이터를 가져오려면:

1. 이전 섹션의 단계를 사용 하 여 WideWorldImporters OLTP 데이터베이스의 데이터 생성 논리를 실행 합니다.
2. 아직 않았다면 WideWorldImportersDW 데이터베이스의 올바른 버전을 설치 합니다. 설치 지침을 참조 하십시오. [설치 및 구성](wide-world-importers-oltp-install-configure.md)합니다.
3. OLAP 데이터베이스는 데이터베이스에 다음 문을 실행 하 여 초기값을 다시 설정 합니다.

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 실행 된 *매일 ETL.ispac* OLAP 데이터베이스로 데이터를 가져오는 SQL Server Integration Services 패키지 합니다. ETL 작업을 실행 하는 방법을 알아보려면 참조 [WideWorldImporters ETL 워크플로](wide-world-importers-perform-etl.md)합니다.

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>성능 테스트를 위한 WideWorldImportersDW에 데이터를 생성

WideWorldImportersDW 성능 테스트에 대 한 데이터 크기를 늘리고 임의로 수 있습니다. 예를 들어 클러스터형된 columnstore 인덱스를 사용 하는 데이터 크기를 늘릴 수 것입니다.

다운로드 크기를 다운로드 하려면를 쉽게 큰 하지만 SQL Server 성능 기능을 설명 하기에 충분 하도록 충분히 작게 유지 하는 과제 중 하나입니다. 예를 들어 더 큰 수의 행으로 작업할 경우에 columnstore 인덱스에 대 한 중요 한 혜택을 높일 수 있습니다. 

사용할 수는 `Application.Configuration_PopulateLargeSaleTable` 프로시저에 있는 행의 수를 늘리려면는 `Fact.Sale` 테이블입니다. 2013 년 1 월 1 일 시작 하는 기존 Wide World Importers 데이터와의 충돌을 방지 하기 위해 2012 역 년에 행 삽입 됩니다.

### <a name="procedure-details"></a>프로시저 세부 정보

#### <a name="name"></a>이름

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>매개 변수

  `@EstimatedRowsFor2012` **bigint** (이며 12000000의 기본값)

#### <a name="result"></a>결과

필요한 행 수 정도에 삽입 되는 `Fact.Sale` 2012 년에는 테이블입니다. 프로시저 하루 50, 000 행의 수를 인위적으로 제한 합니다. 이 제한을 변경할 수는 있지만 한계를 사용 하면 테이블의 실수로 overinflations 방지 합니다.

프로시저에는 클러스터형된 columnstore 인덱스가 이미 적용 되지 않은 경우 적용 됩니다.
