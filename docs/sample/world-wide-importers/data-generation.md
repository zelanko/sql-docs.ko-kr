---
title: "데이터를 생성 | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology:
- " database-engine "
ms.topic: article
ms.assetid: f387273b-8b5f-4687-b033-09499ea2d68f
caps.latest.revision: 
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: 20db5f20256fb4b545482b29b0c5cc41c6ba231e
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 데이터 생성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
이러한 데이터베이스에서 생성 된 하루 최대 년 1 월 1 일부 터 2013을 시작 하는 데이터를 포함 하는 WideWorldImporters 및 WideWorldImportersDW 데이터베이스의 릴리스 버전.

예제 데이터베이스 데모 또는 그림에서는 나중에 사용 되는 경우 데이터베이스의 최신 샘플 데이터를 포함 하는 데 특히 도움이 수도 있습니다.

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

이 문은 현재 날짜 까지의 데이터베이스에 샘플 판매 및 구매 데이터를 추가합니다. 데이터의 진행률 생성 날짜별으로 출력합니다. Rougly 10 분 마다 데이터를 요구 하는 매년 걸립니다. 데이터 생성에는 임의 요인을 이므로 사이 생성 된 데이터의 일부 차이점이에서는 실행 됩니다.

하루에 주문 측면에서 생성 된 데이터의 양을 늘리거나 매개 변수의 값을 변경 `@AverageNumberOfCustomerOrdersPerDay`합니다. 매개 변수 `@SaturdayPercentageOfNormalWorkDay` 및 `@SundayPercentageOfNormalWorkDay` 주말에 대 한 주문 횟수를 결정 하는 데 사용 됩니다.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>WideWorldImportersDW로 생성 된 데이터 가져오기

WideWorldImportersDW OLAP 데이터베이스의 현재 날짜 까지의 샘플 데이터를 가져오려면 다음이 단계를 수행 합니다.

1. 위의 단계를 사용 하 여 WideWorldImporters OLTP 데이터베이스의 데이터 생성 논리를 실행 합니다.
2. 아직 수행 하는 경우 WideWorldImportersDW 데이터베이스의 올바른 버전을 설치 합니다. 설치 지침은 **WideWorldImporters 설치 및 구성**합니다.
3. OLAP 데이터베이스는 데이터베이스에 다음 문을 실행 하 여 초기값을 다시 설정 합니다.

```
    EXECUTE [Application].Configuration_ReseedETL
```

4. SSIS 패키지를 실행 **매일 ETL.ispac** OLAP 데이터베이스로 데이터를 가져옵니다. ETL 작업을 실행 하는 방법에 지침은 **WideWorldImporters ETL 워크플로**합니다.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>성능 테스트를 위한 WideWorldImportersDW에 데이터를 생성

WideWorldImportersDW에 임의로 성능 예를 들어 클러스터 된 columnstore 테스트 목적으로 데이터 크기를 늘리는 기능이 있습니다.

Wide World Importers 다운로드 크기는 배포 가능한 제공 되지만 SQL Server 성능 기능을 보여 주기 위해 수 있을 만큼 큰 충분히 작게 유지 하는 것과 같은 샘플을 배송할 때 과제 중 하나입니다. 여기서는 영역을 하나는 특정 문제는 columnstore 인덱스와 함께 작업 하는 경우. 중요 한 이점이 더 큰 수의 행으로 작업할 때만 제공 됩니다. 

프로시저 `Application.Configuration_PopulateLargeSaleTable` 크게의 행 수를 늘리는 데 사용할 수는 `Fact.Sale` 테이블입니다. Note 행은 2013 년 1 월 1 일에서 시작 하는 기존 Wide World Importers 데이터와의 충돌을 방지 하기 위해 2012 역 년에 삽입 됩니다.

### <a name="procedure-details"></a>프로시저 세부 정보

#### <a name="name"></a>이름: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>매개 변수:

  `@EstimatedRowsFor2012` **bigint** (이며 12000000의 기본값)

#### <a name="result"></a>결과:

필요한 행 수 정도에 삽입 되는 `Fact.Sale` 2012 년에는 테이블입니다. 프로시저 50,000 하루 행 수를 인위적으로 제한 합니다. 이 변경 될 수 있지만 테이블의 실수로 overinflations 방지 하는 것입니다.

또한 프로시저 경우 적용 됩니다 클러스터형된 columnstore 인덱스가 이미 적용 되지 않은 것입니다.
