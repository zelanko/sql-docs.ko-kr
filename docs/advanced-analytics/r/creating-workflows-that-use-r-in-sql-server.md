---
title: "R을 사용 하 여 BI 워크플로 만들기 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624510d814a2b91fdb61d6090abbc673d704d262
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="creating-bi-workflows-with-r"></a>R을 사용 하 여 BI 워크플로 만들기

관계형 데이터베이스는 데이터 쿼리, 저장소, 트랜잭션 처리에 사용되는 확장 가능한 솔루션을 제공하기 위한 고도로 최적화된 기술입니다.

반면, 일반적으로 R 솔루션 일반적으로 했었다면 대개 CSV 형식의 데이터 탐색 및 모델링을 수행할에 다양 한 원본에서 데이터 가져오기. 그러한 작업은 비효율적일 뿐만 아니라 안전하지 않습니다.

이 항목에서는 일반적인 실수 및이 데이터베이스 외부의 시스템 학습 솔루션은 개발 하는 경우 발생할 수 있는 보안 위험을 방지 하는 SQL Server와 함께 R에 대 한 통합 시나리오를 설명 합니다.

비즈니스 인텔리전스 응용 프로그램, 특히 Integration Services 및 Reportng 서비스 R 코드와 상호 작용 및 데이터 또는 그래픽 오른쪽에 의해 생성 된 사용할 수 있는 방법을 예에 대해서도 설명

적용 대상: SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="bring-compute-power-to-the-data"></a>데이터를 계산 능력을 가져와야

기계 학습 SQL Server 통합의 주요 디자인 목표는 데이터에 가까운 분석 했습니다. 이 다음과 같은 여러 이점을 제공합니다.

+ 데이터 보안. 데이터 원본에 가깝게 R 가져오는 낭비 나 안전 하지 않은 데이터 이동을 방지할 수 있습니다.

+ 속도. 데이터베이스는 집합 기반 작업에 최적화됩니다. 데이터 과학에 완벽 한 보완 메모리 내 테이블의 같은 데이터베이스의 최근 혁신 기호와 요약 및 집계를 매우를 확인 하십시오.

+ 배포 및 통합의 용이해 집니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]다른 여러 데이터 관리 작업 및 응용 프로그램에 대 한 작업의 중앙 지점이입니다. 보고 웨어하우스는 데이터베이스에 있는 데이터를 사용 하 여 기계 학습 솔루션에서 사용 하는 데이터 일관성 있고 최신 인지 확인 합니다. 

+ 클라우드 및 온-프레미스에서 효율성입니다. R에서 데이터를 처리하는 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 Azure Data Factory를 비롯한 엔터프라이즈 데이터 파이프라인을 사용할 수 있습니다. Power BI 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 통해 결과 또는 분석을 쉽게 보고할 수 있습니다.

다양한 데이터 처리 및 분석 작업에 SQL과 R을 적절하게 조합하여 사용하면 데이터 과학자와 개발자가 모두 생산성을 높일 수 있습니다.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>데이터에 대 한 Integration Services를 사용 하 여 변환 및 자동화

데이터 과학 워크플로는 반복이 매우 빈번하며, 크기 조정, 집계, 확률 계산, 특성 병합 및 이름 변경을 비롯한 데이터 변환이 많이 이루어집니다. 데이터 과학자는 R, Python 또는 기타 언어로 이러한 작업을 대부분 수행하지만 엔터프라이즈 데이터로 이러한 워크플로를 실행하려면 ETL 도구 및 프로세스와의 원활한 통합이 필요합니다.

Transact-SQL 및 저장 프로시저를 통해 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 R로 복잡한 작업을 실행할 수 있기 때문에 다시 개발하는 작업을 최소화하여 R 작업과 기존 ETL 프로세스를 통합할 수 있습니다. 대신 R에서 메모리 집중형 작업의 체인을 수행 하는 보다 데이터 준비 최적화할 수 등 가장 효율적인 도구를 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 

데이터는 dmodeling 처리를 자동화 하는 방법을 사용 하 여 파이프라인에 대 한 몇 가지 ideass 같습니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 기능을 만들기 위해 필요한 데이터는 SQL 데이터베이스에 대 한 작업
+ 조건부 분기를 사용하여 R 작업에 대한 계산 컨텍스트 전환
+ 데이터베이스에 데이터를 생성 하는 R 작업을 실행 하 고 응용 프로그램과 해당 데이터를 공유 합니다.
+ 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]텍스트 변수로 저장 된 R 스크립트를 로드 하 고 SQL Server에서 실행

### <a name="examples"></a>예

[SQL Server 2016 SSIS 및 R 서비스를 사용하여 기계 학습 프로젝트 운영](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

이 블로그 게시물에 사용 하 여 R 코드를 조작 하는 기본적인 기술을 보여 줍니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ SQL 실행 태스크를 사용 하 여 데이터를 생성 하 고로 저장 하는 R을 호출[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ 저장 프로시저를 사용하여 R 모델을 학습하고 데이터베이스에 저장

+ 스크립트 태스크 및 SQL 실행 태스크를 사용하여 모델에서 점수 매기기 수행

##  <a name="bkmk_ssrs"></a>시각화에 대 한 Reporting Services를 사용 하 여

R로 차트와 흥미로운 시각화를 만들 수 있지만, 외부 데이터 원본과 잘 통합되지 않기 때문에 각 차트와 그래프를 개별적으로 생성해야 합니다. 공유도 어려울 수 있습니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 통해 R로 복잡한 작업을 실행할 수 있기 때문에, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Power BI를 비롯한 다양한 엔터프라이즈 보고 도구에서 쉽게 사용할 수 있습니다.

+ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
+ Power BI에서 테이블 사용

### <a name="examples"></a>예

[Microsoft Reporting Services(SSRS)용 R 그래픽 장치](https://rgraphicsdevice.codeplex.com/)

CodePlex 프로젝트는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에 사용할 수 있는 이미지로 R의 그래픽 출력을 렌더링하는 사용자 지정 보고서 항목을 만드는 데 유용한 코드를 제공합니다.  사용자 지정 보고서 항목을 사용하여 다음을 수행할 수 있습니다.

+ R 그래픽 장치를 사용하여 만든 차트 및 그림을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 대시보드에 게시

+ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 매개 변수를 R 그림에 전달

> [!NOTE]
> 이 샘플에 대 한 Reporting Services에 대 한 R 그래픽 장치를 지 원하는 코드를 Visual Studio에서 뿐만 아니라 Reporting Services 서버에 설치 되어야 합니다. 수동 컴파일 및 구성도 필요합니다.
