---
description: '1단원: SSIS를 사용하여 프로젝트 및 기본 패키지 만들기'
title: '1단원: SSIS를 사용하여 프로젝트 및 기본 패키지 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 428295430a2abb50738742db088b9573a7bf35a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461995"
---
# <a name="lesson-1-create-a-project-and-basic-package-with-ssis"></a>1단원: SSIS를 사용하여 프로젝트 및 기본 패키지 만들기

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



이 단원에서는 단일 플랫 파일 원본에서 데이터를 추출하고 두 개의 조회 변환을 사용하여 데이터를 변환하고, 변환된 데이터를 **AdventureWorksDW2012** 샘플 데이터베이스의 **FactCurrencyRate** 팩트 테이블 사본에 기록하는 간단한 ETL 패키지를 만듭니다. 이 단원에서는 새로운 패키지를 만들고, 데이터 원본 및 대상 연결을 추가 및 구성하고, 새로운 제어 흐름 및 데이터 흐름 구성 요소를 사용하여 작업하는 방법을 알아봅니다.  
  
패키지를 만들기 전에 원본 데이터와 대상 모두에 사용되는 형식을 이해해야 합니다. 그런 다음, 원본 데이터를 대상에 매핑하는 데 필요한 변환을 정의할 수 있습니다.  

## <a name="prerequisites"></a>전제 조건

이 자습서에서는 Microsoft SQL Server Data Tools, 예제 패키지 집합 및 샘플 데이터베이스를 사용합니다.

* SQL Server Data Tools를 설치하려면 [SQL Server Data Tools 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.  
  
* 이 자습서의 모든 단원 패키지를 다운로드하려면:

    1.  [Integration Services 자습서 파일](https://www.microsoft.com/download/details.aspx?id=56827)로 이동합니다.

    2.  **다운로드** 단추를 선택합니다.

    3.  **간단한 ETL Package.zip 만들기** 파일을 선택한 후, **다음**을 선택합니다.

    4.  파일을 다운로드한 후 로컬 디렉터리에 해당 콘텐츠 압축을 풉니다.  

* **AdventureWorksDW2012** 샘플 데이터베이스를 설치 및 배포하려면 [AdventureWorks 샘플 데이터베이스 - SQL 설치 및 구성](../samples/adventureworks-install-configure.md)을 참조하세요.
  
## <a name="look-at-the-source-data"></a>원본 데이터 확인
이 자습서에서 원본 데이터는 **SampleCurrencyData.txt**라는 플랫 파일의 기록 통화 데이터 세트입니다. 원본 데이터에는 평균 통화 비율, 통화 키, 날짜 키, 날짜별 마지막 비율이라는 4개의 열이 있습니다  
  
다음은 SampleCurrencyData.txt 파일의 원본 데이터 예제입니다.  
  
```
1.00070049USD9/3/05 0:001.001201442  
1.00020004USD9/4/05 0:001  
1.00020004USD9/5/05 0:001.001201442  
1.00020004USD9/6/05 0:001  
1.00020004USD9/7/05 0:001.00070049  
1.00070049USD9/8/05 0:000.99980004  
1.00070049USD9/9/05 0:001.001502253  
1.00070049USD9/10/05 0:000.99990001  
1.00020004USD9/11/05 0:001.001101211  
1.00020004USD9/12/05 0:000.99970009
```
  
플랫 파일 원본 데이터를 사용하여 작업할 때는 플랫 파일 연결 관리자가 플랫 파일 데이터를 해석하는 방법을 이해해야 합니다. 플랫 파일 원본이 유니코드일 경우 플랫 파일 연결 관리자가 모든 열을 기본 열 너비 50인 [DT_WSTR]로 정의하고 플랫 파일 원본이 ANSI로 인코딩된 경우 열은 기본 열 너비가 50인 [DT_STR]로 정의합니다. 이러한 기본값을 변경하여 문자열을 데이터에 더 적합한 열 유형으로 만들어야 하는 경우도 있습니다. 대상의 데이터 형식을 확인한 다음, 플랫 파일 연결 관리자 내에서 해당 형식을 선택해야 합니다.  
  
## <a name="look-at-the-destination-data"></a>대상 데이터 확인
원본 데이터의 대상은 **AdventureWorksDW**의 **FactCurrencyRate** 팩트 테이블 복사본입니다. 다음 표와 같이 **FactCurrencyRate** 팩트 테이블에는 4개의 열이 있으며 두 차원 테이블에 대한 관계가 있습니다.  
  
|열 이름|데이터 형식|조회 테이블|조회 열|  
|---------------|-------------|----------------|-----------------|  
|AverageRate|float|None|없음|  
|CurrencyKey|int(FK)|DimCurrency|CurrencyKey(PK)|  
|DateKey|int(FK)|FactOnlineSales|DateKey (PK)|  
|EndOfDayRate|float|None|없음|  
  
## <a name="map-the-source-data-to-the-destination"></a>원본 데이터를 대상에 매핑  
원본 및 대상 데이터 형식의 분석에는 **CurrencyKey** 및 **DateKey** 값에 대한 조회가 필요함을 나타냅니다. 이러한 조회를 수행하는 변환은 **DimCurrency** 및 **DimDate** 차원 테이블의 대체 키를 사용하여 해당 값을 가져옵니다.  
  
|플랫 파일 열|테이블 이름|열 이름|데이터 형식|  
|--------------------|--------------|---------------|-------------|  
|0|FactCurrencyRate|AverageRate|float|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|FactOnlineSales|FullDateAlternateKey|date|  
|3|FactCurrencyRate|EndOfDayRate|float|  
  
## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 새 Integration Services 프로젝트 만들기](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [2단계: 플랫 파일 연결 관리자 추가 및 구성](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [3단계: OLE DB 연결 관리자 추가 및 구성](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [4단계: 패키지에 데이터 흐름 태스크 추가](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [5단계: 플랫 파일 원본 추가 및 구성](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [6단계: 조회 변환 추가 및 구성](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [7단계: OLE DB 대상 추가 및 구성](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [8단계: 1단원 패키지 주석 달기 및 형식](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [9단계: 1단원 패키지 테스트](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 새 통합 서비스 프로젝트 만들기](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
