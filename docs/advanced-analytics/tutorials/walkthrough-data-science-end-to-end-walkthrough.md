---
title: "R 및 SQL Server에 대 한 종단 간 데이터 과학 연습 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a49cad5bd89633841c5ff54c03e39b098fca72e5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>R및 SQL Server용 데이터 과학 전체 과정 연습

이 연습에서는 SQL Server 2016 또는 SQL Server 2017에서 Microsoft R 기반 예측 모델링을 위한 전체 솔루션을 개발합니다.

이 연습은 공용 데이터 중 많이 사용되는 뉴욕 시 택시 데이터 집합을 기반으로 합니다. R 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SQL Server 데이터, 사용자 지정 SQL 함수를 사용하여 분류 모델을 작성하고 이를 통해 택시 운전사가 팁을 얻을 수 있는지 그 가능성을 예측합니다. 또한 R 모델을 SQL Server에 배포하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 데이터를 사용해서 해당 모델에 기반한 점수(score)를 생성 합니다.

이 예제는 영업 캠페인에 대한 고객 반응 예측, 특정 행사의 비용 지출이나 참석 예측과 같은 모든 유형의 실제 문제로 확장될 수 있습니다. 저장 프로시저를 통해 예측 모델을 호출할 수 있으므로 응용 프로그램에 쉽게 내장할 수 있습니다.

이 연습은 R 개발자들에게 R Services(In-Database)를 소개하기 위해 설계되었음으로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R이 가능한 모든 곳에 사용됩니다. 그러나 이것이 R이 항상 모든 작업에서 가장 좋은 도구임을 의미하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 집계나 특성(feature) 엔지니어링같은 특정 작업에서는 대부분 SQL Server가 더 나은 성능을 제공할 것입니다. 특히 메모리 최적화 columnstore 인덱스 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인덱스와 같은 SQL Server 2017의 새로운 기능들이 도움이 될 수 있습니다. 과정을 거치면서 가용한 최적화 방안들을 언급할 것입니다.

> [!NOTE]
> 이 연습은 원래 SQL Server 2016용으로 개발하고 시험했습니다만, 스크린 샷과 프로시저들은 SQL Server 2017 에서도 작동할 수 있도록 최신 버전의 SQL Server Management Studio를 사용해서 업데이트 했습니다.

## <a name="overview"></a>개요

아래 예상 시간에 설치 작업은 포함되지 않습니다. 자세한 내용은 [연습에 대 한 필수 구성 요소](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)를 참조하세요.

|항목 목록|예상 시간|
|-|------------------------------|
|[R 연습 데이터 준비](../tutorials/walkthrough-prepare-the-data.md) <br /><br />모델 작성에 사용되는 데이터를 가져옵니다. 공용 데이터 집합을 다운로드하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 로드합니다.|30분|
|[SQL을 사용하여 데이터 탐색](../tutorials/walkthrough-view-and-explore-the-data.md) <br /><br />SQL 도구와 요약을 사용하여 데이터를 이해합니다.|10분|
|[R을 사용하여 데이터 요약](../tutorials/walkthrough-view-and-summarize-data-using-r.md) <br /><br />R을 사용 하 여 데이터를 탐색 하 고 요약을 생성 합니다.|10분|
|[SQL Server에서 R을 사용하여 plot 만들기](../tutorials/walkthrough-create-graphs-and-plots-using-r.md) <br /><br />R및 SQL을 혼합하여 로컬 및 원격 계산 컨텍스트에서 plot을 만듭니다.|10분|
|[R과 T-SQL을 사용하여 데이터 기능을 만들기)](../tutorials/walkthrough-create-data-features.md) <br /><br />R과 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 지정 함수를 사용하여 특성 공학(feature engineering)을 수행합니다.  특성 공학 작업에서의 R및 T-SQL의 성능을 비교하십시오. |10분|
|[R 모델을 작성하고 SQL Server에 저장](../tutorials/walkthrough-build-and-save-the-model.md) <br /><br />예측 모델 학습과 튜닝. 모델 성능을 평가. 이 연습에서는 분류 모델을 만듭니다. R을 사용하여 모델의 정확도를 그립니다.|15분|
|[SQL Server를 사용하여 R 모델 배포](../tutorials/walkthrough-deploy-and-use-the-model.md) <br /><br />모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하여 프로덕션에 모델을 배포합니다. 저장 프로시저에서 모델을 호출하여 예측을 생성합니다.|10분|

### <a name="intended-audience"></a>대상 독자

이 연습은 R 또는 SQL 개발자를 위한 것입니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 사용하여 엔터프라이즈 워크플로에 R을 통합하는 방법을 소개합니다. 데이터베이스와 테이블 만들기, 데이터 가져오기, 쿼리 실행 같은 데이터베이스 작업에 익숙해야 합니다.

+ 모든 SQL과 R 스크립트가 포함됩니다.
+ 사용자 환경에서 실행하려면 스크립트내 문자열을 수정할 필요도 있습니다. [Visual Studio Code](https://code.visualstudio.com/Download)같은 코드 편집기로 이러한 작업을 수행할 수 있습니다.

### <a name="prerequisites"></a>필수 구성 요소

+ SQL Server 2016의 인스턴스 또는 SQL Server 2017의 평가 버전에 액세스할 수 있어야 합니다.
+	SQL Server 인스턴스에 최소 하나의 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]가 설치되어 있어야 합니다.
+ 랩톱이나 다른 네트워크 컴퓨터 같은 원격 컴퓨터에서 R 명령을 실행하려면 Microsoft R Open 라이브러리를 설치해야 합니다. Microsoft R 클라이언트 또는 Microsoft R Server를 설치할 수 있습니다. 원격 컴퓨터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있어야 합니다.
+ 동일한 컴퓨터에 클라이언트와 서버를 둘 경우 "원격" 클라이언트에서 R 스크립트를 보내는데 사용할 별도의 Microsoft R 라이브러리 집합을 설치하십시오. SQL Server 인스턴스용으로 설치된 R 라이브러리를 이 목적으로 사용하지 마십시오.

서버 및 클라이언트 환경을 설정하는 자세한 방법은 [R 및 SQL Server 데이터 과학 연습에 대한 필수 구성 요소](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)를 참조하십시오.

## <a name="next-lesson"></a>다음 단원

[R 연습 데이터 준비](../tutorials/walkthrough-prepare-the-data.md)
