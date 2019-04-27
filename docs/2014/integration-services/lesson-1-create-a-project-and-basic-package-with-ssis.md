---
title: '1단원: 프로젝트 및 기본 패키지 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 652cf44f70e890b3203ed27890d06f98d70b7f1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767505"
---
# <a name="lesson-1-creating-the-project-and-basic-package"></a>1단원: 프로젝트 및 기본 패키지 만들기
  이 단원에서는 하나의 플랫 파일 원본에서 데이터를 추출하고 두 개의 조회 변환 구성 요소를 사용하여 데이터를 변환하며 **AdventureWorksDW2012** 의 **FactCurrency**팩트 테이블에 해당 데이터를 쓰는 간단한 ETL 패키지를 만듭니다. 이 단원에서는 새로운 패키지를 만들고 데이터 원본 및 대상 연결을 추가하고 구성하며 새로운 제어 흐름 및 데이터 흐름 구성 요소를 사용하여 작업하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. 설치 및 배포에 대 한 자세한 내용은 **AdventureWorksDW2012**를 참조 하세요 [Microsoft SQL Server Product Samples: Reporting Services](https://archive.codeplex.com/?p=msftrsprodsamples).  
  
## <a name="understanding-the-package-requirements"></a>패키지 요구 사항 이해  
 이 자습서를 사용하려면 Microsoft SQL Server Data Tools가 필요합니다.  
  
 SQL Server Data Tools 설치 방법에 대한 자세한 내용은 [SQL Server Data Tools 다운로드](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017)를 참조하세요.  
  
 패키지를 만들기 전에 원본 데이터와 대상 양쪽에 사용되는 형식을 제대로 알아야 합니다. 이러한 데이터 형식을 모두 파악하면 원본 데이터를 대상에 매핑하는 데 필요한 변환을 정의할 수 있습니다.  
  
### <a name="looking-at-the-source"></a>원본 확인  
 이 자습서에서 원본 데이터는 플랫 파일인 SampleCurrencyData.txt에 포함된 기록 통화 데이터 집합입니다. 원본 데이터에는 평균 통화 비율, 통화 키, 날짜 키, 날짜별 마지막 비율이라는 4개의 열이 있습니다  
  
 다음은 SampleCurrencyData.txt 파일에 포함된 원본 데이터의 예입니다.  
  
 `1.00070049USD9/3/05 0:001.001201442`  
  
 `1.00020004USD9/4/05 0:001`  
  
 `1.00020004USD9/5/05 0:001.001201442`  
  
 `1.00020004USD9/6/05 0:001`  
  
 `1.00020004USD9/7/05 0:001.00070049`  
  
 `1.00070049USD9/8/05 0:000.99980004`  
  
 `1.00070049USD9/9/05 0:001.001502253`  
  
 `1.00070049USD9/10/05 0:000.99990001`  
  
 `1.00020004USD9/11/05 0:001.001101211`  
  
 `1.00020004USD9/12/05 0:000.99970009`  
  
 플랫 파일 원본 데이터를 사용하여 작업할 때는 플랫 파일 연결 관리자가 플랫 파일 데이터를 해석하는 방법을 이해해야 합니다. 플랫 파일 원본이 유니코드일 경우 플랫 파일 연결 관리자가 모든 열을 기본 열 너비 50인 [DT_WSTR]로 정의하고 플랫 파일 원본이 ANSI로 인코딩된 경우 열 너비 50인 [DT_STR]로 정의합니다. 이 기본값을 변경하여 문자열을 데이터에 알맞은 열 유형으로 만들어야 하는 경우도 있습니다. 이렇게 하려면 데이터가 쓰여지는 대상의 데이터 형식을 확인한 다음 플랫 파일 연결 관리자에서 알맞은 형식을 선택해야 합니다.  
  
### <a name="looking-at-the-destination"></a>대상 확인  
 원본 데이터의 궁극적인 대상은 **AdventureWorksDW** 의 **FactCurrency**팩트 테이블입니다. 다음 표와 같이 **FactCurrency** 팩트 테이블에는 4개의 열이 있으며 두 차원 테이블에 대한 관계가 있습니다.  
  
|열 이름|데이터 형식|조회 테이블|조회 열|  
|-----------------|---------------|------------------|-------------------|  
|AverageRate|FLOAT|없음|없음|  
|CurrencyKey|int(FK)|DimCurrency|CurrencyKey(PK)|  
|DateKey|int(FK)|FactOnlineSales|DateKey (PK)|  
|EndOfDayRate|FLOAT|없음|없음|  
  
### <a name="mapping-source-data-to-be-compatible-with-the-destination"></a>대상과 호환될 원본 데이터 매핑  
 원본 및 대상 데이터 형식을 분석하면 **CurrencyKey** 와 **DateKey** 값을 조회해야 한다는 사실을 알 수 있습니다. 이러한 조회를 수행할 변환은 **DimCurrency** 및 **DimDate** 차원 테이블의 대체 키를 사용하여 **CurrencyKey** 및 **DateKey** 값을 가져옵니다.  
  
|플랫 파일 열|테이블 이름|열 이름|데이터 형식|  
|----------------------|----------------|-----------------|---------------|  
|0|AdventureWorksDW2012|AverageRate|float|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|FactOnlineSales|FullDateAlternateKey|date|  
|3|AdventureWorksDW2012|EndOfDayRate|FLOAT|  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 새 Integration Services 프로젝트 만들기](lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [2단계: 플랫 파일 연결 관리자 추가 및 구성](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [3단계: 추가 하 고 OLE DB 연결 관리자 구성](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [4단계: 패키지에 데이터 흐름 태스크 추가](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [5단계: 플랫 파일 원본 추가 및 구성](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [6단계: 조회 변환 추가 및 구성](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [7단계: OLE DB 대상 추가 및 구성](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [8단계: 1 단원 패키지를 보다 쉽게 이해](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [9단계: 1 단원 자습서 패키지 테스트](lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
 [1단계: 새 Integration Services 프로젝트 만들기](lesson-1-1-creating-a-new-integration-services-project.md)  
  
  
