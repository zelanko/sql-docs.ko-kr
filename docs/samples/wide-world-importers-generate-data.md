---
title: 데이터 요금-SQL 샘플 데이터베이스를 생성 하는 WideWorldImporters | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- " database-engine "
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: d99cdfacbe08cd3b81fb46bb61b49cab290780f4
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 데이터 생성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
이러한 데이터베이스에서 생성 된 하루 최대 년 1 월 1 2013을 시작 하는 데이터를 포함 하는 WideWorldImporters 및 WideWorldImportersDW 데이터베이스의 릴리스 버전.

예제 데이터베이스를 사용할 때는 최신 샘플 데이터를 포함 하는 데 특히 도움이 수도 있습니다.

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters에서 데이터 생성

현재 날짜 까지의 샘플 데이터를 생성 하려면 다음이 단계를 따르십시오.

1. 아직 수행 하는 경우에 WideWorldImporters 데이터베이스의 정리 버전이 설치 합니다. 설치 지침은 **WideWorldImporters 설치 및 구성**합니다.
2. 데이터베이스에 다음 문을 실행 합니다.

```
    EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
        @AverageNumberOfCustomerOrdersPerDay = 60,
        @SaturdayPercentageOfNormalWorkDay = 50,
        @SundayPercentageOfNormalWorkDay = 0,
        @IsSilentMode = 1,
        @AreDatesPrinted = 1;
```

이 문은 현재 날짜 까지의 데이터베이스에 샘플 판매 및 구매 데이터를 추가합니다. 데이터의 진행률 생성 날짜별으로 출력합니다. 에 대 한 데이터를 요구 하는 매년 약 10 분 정도 걸릴 수 있습니다. 데이터 생성에는 임의 요인을 이므로 실행 사이 생성 된 데이터의 차이가 있습니다.

하루에 주문 측면에서 생성 된 데이터의 양을 늘리거나 매개 변수의 값을 변경 `@AverageNumberOfCustomerOrdersPerDay`합니다. 매개 변수 `@SaturdayPercentageOfNormalWorkDay` 및 `@SundayPercentageOfNormalWorkDay` 주말에 대 한 주문 횟수를 결정 하는 데 사용 됩니다.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>WideWorldImportersDW로 생성 된 데이터 가져오기

WideWorldImportersDW OLAP 데이터베이스의 현재 날짜 까지의 샘플 데이터를 가져오려면 다음이 단계를 수행 합니다.

1. 위의 단계를 사용 하 여 WideWorldImporters OLTP 데이터베이스의 데이터 생성 논리를 실행 합니다.
2. 아직 수행 하는 경우 WideWorldImportersDW 데이터베이스의 올바른 버전을 설치 합니다. 설치 지침은 **WideWorldImporters 설치 및 구성**합니다.
3. OLAP 데이터베이스는 데이터베이스에 다음 문을 실행 하 여 초기값을 다시 설정 합니다.

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. SSIS 패키지를 실행 **매일 ETL.ispac** OLAP 데이터베이스로 데이터를 가져옵니다. ETL 작업을 실행 하는 방법에 지침은 **WideWorldImporters ETL 워크플로**합니다.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>성능 테스트를 위한 WideWorldImportersDW에 데이터를 생성

WideWorldImportersDW에 임의로 성능 예를 들어 클러스터 된 columnstore 테스트 목적으로 데이터 크기를 늘리는 기능이 있습니다.

다운로드 크기를 다운로드 하려면를 쉽게 큰 하지만 SQL Server 성능 기능을 설명 하기에 충분 하도록 충분히 작게 유지 하는 과제 중 하나입니다. 예를 들어, columnstore 인덱스에 대 한 상당한 혜택이 더 큰 수의 행으로 작업할 때만 발생 합니다. 

프로시저 `Application.Configuration_PopulateLargeSaleTable` 크게의 행 수를 늘리는 데 사용할 수는 `Fact.Sale` 테이블입니다. Note 행은 2013 년 1 월 1부터 시작 하는 기존 Wide World Importers 데이터와의 충돌을 방지 하기 위해 2012 역 년에 삽입 됩니다.

### <a name="procedure-details"></a>프로시저 세부 정보

#### <a name="name"></a>이름: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>매개 변수:

  `@EstimatedRowsFor2012` **bigint** (이며 12000000의 기본값)

#### <a name="result"></a>결과:

필요한 행 수 정도에 삽입 되는 `Fact.Sale` 2012 년에는 테이블입니다. 프로시저 50,000 하루 행 수를 인위적으로 제한 합니다. 이 제한 수는 변경할 수 있지만 테이블의 실수로 overinflations 방지 하는 것입니다.

또한 프로시저 경우 적용 됩니다 클러스터형된 columnstore 인덱스가 이미 적용 되지 않은 것입니다.
