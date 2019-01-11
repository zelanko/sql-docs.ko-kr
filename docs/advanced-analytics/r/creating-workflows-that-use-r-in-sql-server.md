---
title: R-SQL Server Machine Learning Services를 사용 하 여 비즈니스 인텔리전스 (BI) 워크플로 만들기
description: SQL Server 및 SQL Server Integration Services (SSIS)에서 비즈니스 인텔리전스 (BI) 및 R 언어를 결합 하는 통합 시나리오 지원 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 32dfb3317cb790c19289ab02362bf8ee765e5259
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432736"
---
# <a name="creating-bi-workflows-with-r"></a>R을 사용 하 여 BI 워크플로 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

관계형 데이터베이스는 데이터 쿼리, 스토리지, 트랜잭션 처리에 사용되는 확장 가능한 솔루션을 제공하기 위한 고도로 최적화된 기술입니다.

반면, 일반적으로 R 솔루션 일반적으로 의존 대개 CSV 형식으로 데이터 탐색 및 모델링 하는 데에 다양 한 원본에서 데이터 가져오기. 그러한 작업은 비효율적일 뿐만 아니라 안전하지 않습니다.

이 문서에서는 일반적인 문제 및 기계 학습 솔루션은 데이터베이스 외부의 개발 하는 경우 발생할 수 있는 보안 위험을 방지 하는 SQL Server를 사용 하 여 R에 대 한 통합 시나리오를 설명 합니다.

비즈니스 인텔리전스 응용 프로그램, 특히: Integration Services 및 Reporting Services, R 코드와 상호 작용 및 데이터 또는 R에서 생성 하는 그래픽을 사용할 수 있는 방법을 예제에 대해서도 설명

적용 대상: SQL Server 2016 R Services, SQL Server 2017 Machine Learning 서비스

## <a name="bring-compute-power-to-the-data"></a>데이터에 계산 능력을 가져오기

SQL Server를 사용 하 여 machine learning을 통합 하는 주요 디자인 목표를 분석 데이터에 근접 했습니다. 다음과 같은 여러 이점을 제공 합니다.

+ 데이터 보안. 데이터 원본에 더 가까운 곳에 R을 가져오는 불필요 하거나 안전 하지 않은 데이터 이동을 방지할 수 있습니다.

+ 속도. 데이터베이스는 집합 기반 작업에 최적화됩니다. 메모리 내 테이블에 같은 데이터베이스의 최신 혁신 요약 및 번개, 집계 및 데이터 과학을 완벽 하 게 보완 됩니다.

+ 배포 및 통합 편의성입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다른 많은 데이터 관리 작업 및 응용 프로그램에 대 한 작업의 중앙 지점이입니다. 보고 웨어하우스 데이터베이스에 있는 데이터를 사용 하 여 기계 학습 솔루션에서 사용 하는 데이터가 일관성 있고 최신 인지 확인 합니다. 

+ 클라우드 및 온-프레미스에서 효율성입니다. R에서 데이터를 처리하는 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 Azure Data Factory를 비롯한 엔터프라이즈 데이터 파이프라인을 사용할 수 있습니다. Power BI 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 통해 결과 또는 분석을 쉽게 보고할 수 있습니다.

다양한 데이터 처리 및 분석 작업에 SQL과 R을 적절하게 조합하여 사용하면 데이터 과학자와 개발자가 모두 생산성을 높일 수 있습니다.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>데이터에 대 한 Integration Services를 사용 하 여 변환 및 자동화

데이터 과학 워크플로는 반복이 매우 빈번하며, 크기 조정, 집계, 확률 계산, 특성 병합 및 이름 변경을 비롯한 데이터 변환이 많이 이루어집니다. 데이터 과학자는 R, Python 또는 기타 언어로 이러한 작업을 대부분 수행하지만 엔터프라이즈 데이터로 이러한 워크플로를 실행하려면 ETL 도구 및 프로세스와의 원활한 통합이 필요합니다.

Transact-SQL 및 저장 프로시저를 통해 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 R로 복잡한 작업을 실행할 수 있기 때문에 다시 개발하는 작업을 최소화하여 R 작업과 기존 ETL 프로세스를 통합할 수 있습니다. 대신 R에서 메모리 집중형 작업의 체인을 수행 하는 보다 데이터 준비를 최적화할 수 있습니다를 비롯 한 가장 효율적인 도구를 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 고 [!INCLUDE[tsql](../../includes/tsql-md.md)]입니다. 

다음은 데이터 처리를 자동화할 수 있습니다 하는 방법에 대 한 몇 가지 아이디어 및 모델링에 사용 하 여 파이프라인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SQL database에 필요한 데이터 기능 만들기 작업
+ 조건부 분기를 사용하여 R 작업에 대한 계산 컨텍스트 전환
+ 데이터베이스에서 자신의 데이터를 생성 하는 R 작업을 실행 하 고 응용 프로그램을 사용 하 여 해당 데이터를 공유 합니다.
+ 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 텍스트 변수로 저장 된 R 스크립트를 로드 및 SQL Server에서 실행

### <a name="examples"></a>예

[SQL Server 2016 SSIS 및 R 서비스를 사용하여 기계 학습 프로젝트 운영](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

이 블로그 게시물을 사용 하 여 R 코드를 조작 하는 기본적인 기술을 보여 줍니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ SQL 실행 태스크를 사용 하 여 데이터를 생성 하 고에 저장 된 R 호출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ 저장 프로시저를 사용하여 R 모델을 학습하고 데이터베이스에 저장

+ 스크립트 태스크 및 SQL 실행 태스크를 사용하여 모델에서 점수 매기기 수행

##  <a name="bkmk_ssrs"></a> 시각화를 위한 Reporting Services를 사용 합니다.

R로 차트와 흥미로운 시각화를 만들 수 있지만, 외부 데이터 원본과 잘 통합되지 않기 때문에 각 차트와 그래프를 개별적으로 생성해야 합니다. 공유도 어려울 수 있습니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 통해 R로 복잡한 작업을 실행할 수 있기 때문에, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Power BI를 비롯한 다양한 엔터프라이즈 보고 도구에서 쉽게 사용할 수 있습니다.

+ 사용 하 여 R 스크립트에서 반환 된 그래픽 개체 시각화 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
+ Power BI에서 테이블 사용

### <a name="examples"></a>예

[Microsoft Reporting Services(SSRS)용 R 그래픽 장치](https://rgraphicsdevice.codeplex.com/)

CodePlex 프로젝트는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에 사용할 수 있는 이미지로 R의 그래픽 출력을 렌더링하는 사용자 지정 보고서 항목을 만드는 데 유용한 코드를 제공합니다.  사용자 지정 보고서 항목을 사용하여 다음을 수행할 수 있습니다.

+ R 그래픽 디바이스를 사용하여 만든 차트 및 그림을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 대시보드에 게시

+ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 매개 변수를 R 그림에 전달

> [!NOTE]
> 이 샘플에서는 Reporting Services 용 R 그래픽 장치를 지 원하는 코드를 Visual Studio 및 Reporting Services 서버에 설치 되어야 합니다. 수동 컴파일 및 구성도 필요합니다.
