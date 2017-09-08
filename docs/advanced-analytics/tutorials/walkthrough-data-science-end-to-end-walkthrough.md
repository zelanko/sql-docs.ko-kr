---
title: "R 및 SQL Server에 대 한 종단 간 데이터 과학 연습 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a49cad5bd89633841c5ff54c03e39b098fca72e5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>R 및 SQL Server에 대 한 종단 간 데이터 과학 연습

이 연습에서는 SQL Server 2016 또는 SQL Server 2017 Microsoft R에 따라 예측 모델링에 대 한 종단 간 솔루션을 개발 합니다.

이 연습은 많이 사용되는 공용 데이터 집합인 뉴욕 시 택시 데이터 집합을 기반으로 합니다. R 코드의 조합을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 및 사용자 지정 SQL 함수는 드라이버 특정 택시 여행 팁을 얻을 수 있습니다 가능성을 나타내는 분류 모델을 작성 합니다. R 모델을 배포할 수도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 데이터를 사용 하 여 모델을 기반으로 점수를 생성 합니다.

이 예제에서는 모든 종류의 판매 캠페인에 대 한 고객 응답을 예측 또는 예측 지출 또는 원하는 경우 참석 해도 행사에서 같은 실제 비즈니스 문제를 확장할 수 있습니다. 저장된 프로시저에서 모델을 호출할 수 있습니다, 때문에 응용 프로그램에서 쉽게 포함할 수 있습니다.

이 연습에서는 개발자가 R을 소개 하기 위한 설계 되었기 때문에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R 가능한 경우 항상 사용 됩니다. 그러나 R은 각 작업에 대해 가장 적합 한 도구 반드시이 아닙니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 대부분의 경우, 특히 데이터 집계, 기능 엔지니어링 등의 작업에서 더 나은 성능을 제공할 수 있습니다.  이러한 작업은 메모리 액세스에 최적화된 columnstore 인덱스 등 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 새로운 기능을 활용할 수 있습니다. 이 과정에서 가능한 최적화 지적 하려고 합니다.

> [!NOTE]
> 이 연습은 원래 SQL Server 2016용으로 개발 및 테스트되었습니다. 그러나 스크린샷 및 프로시저 최신 버전의 SQL Server 2017 함께 작동 하 여 SQL Server Management Studio를 사용 하도록 업데이트 되었습니다.

## <a name="overview"></a>개요

예상 시간은 설치 프로그램을 포함 하지 마세요. 자세한 내용은 참조 [연습에 대 한 필수 구성 요소](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)합니다.

|항목 목록|예상 시간|
|-|------------------------------|
|[R 연습 데이터 준비](../tutorials/walkthrough-prepare-the-data.md) <br /><br />모델 작성에 사용되는 데이터를 가져옵니다. 공용 데이터 집합을 다운로드하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 로드합니다.|30분|
|[SQL을 사용 하 여 데이터 탐색](../tutorials/walkthrough-view-and-explore-the-data.md) <br /><br />SQL 도구 및 요약을 사용 하 여 데이터를 이해 합니다.|10분|
|[R을 사용 하 여 데이터를 요약](../tutorials/walkthrough-view-and-summarize-data-using-r.md) <br /><br />R을 사용 하 여 데이터를 탐색 하 고 요약을 생성 합니다.|10분|
|[SQL Server에서 R을 사용 하 여 점도 만들기](../tutorials/walkthrough-create-graphs-and-plots-using-r.md) <br /><br />R과 SQL을 혼합 하 여 로컬 및 원격 계산 컨텍스트에서 플롯을 만듭니다.|10분|
|[R 및 T-SQL을 사용 하 여 데이터 기능을 만들기)](../tutorials/walkthrough-create-data-features.md) <br /><br />R과 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 지정 함수를 사용하여 기능 엔지니어링을 수행합니다. 기능 작업에 대한 R 및 T-SQL의 성능을 비교합니다. |10분|
|[R 모델을 작성 하 고 SQL Server에 저장](../tutorials/walkthrough-build-and-save-the-model.md) <br /><br />예측 모델을 학습 및 튜닝합니다. 모델 성능을 평가합니다. 이 연습에서는 분류 모델을 만듭니다. R을 사용하여 모델의 정확도를 그립니다.|15분|
|[SQL Server를 사용 하 여 R 모델 배포](../tutorials/walkthrough-deploy-and-use-the-model.md) <br /><br />모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하여 프로덕션에 모델을 배포합니다. 저장 프로시저에서 모델을 호출하여 예측을 생성합니다.|10분|

### <a name="intended-audience"></a>적용 대상

이 연습은 R 또는 SQL 개발자를 위해 작성되었습니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 엔터프라이즈 워크플로에 R을 통합하는 방법을 소개합니다.  데이터베이스 및 테이블 만들기, 데이터를 가져오는 경우, 쿼리 실행 등의 데이터베이스 작업에 익숙해야 합니다.

+ 모든 SQL과 R 스크립트가 포함 되어 있습니다.
+ 사용자 환경에서 실행 하는 스크립트에서 문자열을 수정 해야 합니다. 이렇게 하려면 코드 편집기와 같은 [Visual Studio Code](https://code.visualstudio.com/Download)합니다.

### <a name="prerequisites"></a>필수 구성 요소

+ SQL Server 2016의 인스턴스 또는 SQL Server 2017의 평가 버전에 액세스할 수 있어야 합니다.
+ 하나 이상의 SQL Server 컴퓨터 인스턴스에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]이 설치되어 있어야 합니다.
+ 랩톱 등의 원격 컴퓨터 또는 다른 네트워크로 연결 된 컴퓨터에서 R 명령을 실행 하려는 경우에 Microsoft R Open 라이브러리를 설치 해야 합니다. Microsoft R Client 또는 Microsoft R Server를 설치할 수 있습니다. 원격 컴퓨터에 연결할 수 있어야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.
+ 동일한 컴퓨터에 클라이언트와 서버를 배치 해야 할 경우에 "원격" 클라이언트에서 R 스크립트에서 사용 하기 위해 Microsoft R 라이브러리 별도 집합을 설치 해야 합니다. 사용 하지 마십시오 설치 된 R 라이브러리 사용 하기 위해 SQL Server 인스턴스에서이 목적을 위해.

이러한 서버 및 클라이언트 환경을 설정 하는 방법에 대 한 세부 정보를 참조 하십시오. [R 및 SQL Server 데이터 과학 연습에 대 한 필수 구성 요소](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)합니다.

## <a name="next-lesson"></a>다음 단원

[R 연습 데이터 준비](../tutorials/walkthrough-prepare-the-data.md)

