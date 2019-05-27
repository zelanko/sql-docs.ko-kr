---
title: SQL Server 용 데이터 마이닝 추가 기능의 Office | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c9021a19-2c19-4f0a-a293-5f7e0ac2524c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 10015ac40948c95f8c912ba6fdb71147e50bb880
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082886"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>Office용 SQL Server 데이터 마이닝 추가 기능
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Office용 데이터 마이닝 추가 기능은 Excel의 데이터를 사용하여 예측, 권장 또는 탐색을 위한 분석 모델을 작성할 수 있도록 지원하는 일련의 간단한 예측 분석 도구 집합입니다.  
  
 추가 기능의 마법사 및 데이터 관리 도구는 다음과 같은 일반 데이터 마이닝 작업에 대한 단계별 지침을 제공합니다.  
  
-   **모델링하기 전에 데이터를 구성 및 정리합니다.** Excel 또는 Excel 데이터 원본에 저장된 데이터를 사용합니다. 연결을 만들어 저장한 후 데이터 원본을 다시 사용하거나 실험을 반복하거나 모델을 다시 학습시킬 수 있습니다.  
  
-   **프로필을 만들고 샘플링하고 준비합니다.** 많은 데이터 마이닝 전문가에 따르면 데이터 마이닝 프로젝트의 70-90퍼센트가 데이터 준비에 소모됩니다. 추가 기능은 다음과 같은 일반 작업에 도움이 되는 마법사와 Excel의 시각화 기능을 제공하여 데이터 준비 작업이 보다 빠르게 진행될 수 있도록 합니다.  
  
    -   데이터를 프로파일링하고 데이터의 분포 및 특성을 이해합니다.  
  
    -   무작위 샘플링이나 초과 샘플링을 통해 학습 및 테스트 집합을 만듭니다.  
  
    -   이상값을 찾아 제거하거나 대체합니다.  
  
    -   데이터에 레이블을 다시 지정하여 분석 품질을 높입니다.  
  
-   **감독 또는 자율 학습을 통해 패턴을 분석합니다.** 편리한 마법사를 클릭하면서 클러스터링 분석, 시장 바구니 분석 및 예측 등 몇 가지 가장 널리 사용되는 데이터 마이닝 작업을 수행합니다.  
  
     추가 기능에 포함된 잘 알려진 시스템 학습 알고리즘 중에는 Naïve Bayes, 로지스틱 회귀, 클러스터링, 시계열 및 신경망이 있습니다.  
  
     데이터 마이닝이 처음이라면 **쿼리** 마법사의 도움을 받아 예측 쿼리를 작성해 보십시오.  
  
     고급 사용자는 끌어서 놓기 **고급 쿼리 편집기**를 사용하여 사용자 지정 DMX 쿼리를 작성하거나 Excel VBA를 사용하여 예측을 자동화할 수 있습니다.  
  
-   **문서화하고 관리합니다.** 데이터 집합을 만들고 일부 모델을 작성 한 후 데이터 및 모델 매개 변수의 통계 요약을 생성 하 여 작업과 통찰을 문서화 합니다.  
  
-   **탐색하고 시각화합니다.** 데이터 마이닝 완벽 하 게 자동화할 수 있는 활동이 아닙니다.-탐색 하 고 의미 있는 작업을 수행 하 여 결과 이해 해야 합니다. 추가 기능은 Excel의 대화형 뷰어, 모델 다이어그램을 사용자 지정할 수 있는 Visio 템플릿, 추가 필터링이나 수정을 위해 차트와 테이블을 Excel로 내보내는 기능을 제공하므로 탐색하는 데 도움이 됩니다.  
  
-   **배포하고 통합합니다.** 실험 서버에서 모델의 다른 인스턴스를 내보내려면 관리 도구를 사용 하 여 프로덕션 환경으로 배치 하는 유용한 모델을 만든 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
     또는 모델을 만든 서버에 모델을 그대로 두되 학습 데이터를 새로 고치고 Integration Services 또는 DMX 스크립트를 사용하여 예측을 실행할 수도 있습니다.  
  
     고급 사용자는 서버로 전송된 XMLA 및 DMX 문을 표시하는 **추적** 기능을 유용하게 여길 것입니다.  
  
## <a name="getting-started"></a>시작하기  
 도구에 대해 알아보고 도구를 설정하려면 다음 항목을 참조하십시오.  
  
-   [Excel 용 데이터 마이닝 클라이언트 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](../data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
-   [Excel용 테이블 분석 도구](../table-analysis-tools-for-excel.md)  
  
-   [Visio용 데이터 마이닝 셰이프](../data-mining-shapes-for-visio.md)  
  
-   [데이터 마이닝 서버에 연결](../connect-to-a-data-mining-server.md)  
  
## <a name="support-and-requirements"></a>지원 및 요구 사항  
 Office용 SQL Server 데이터 마이닝 추가 기능은 무료로 다운로드할 수 있습니다. 이러한 도구를 사용하려면 다음 Office 버전 중 하나가 이미 설치되어 있어야 합니다.  
  
-   Office 2010, 32비트 또는 64비트 버전  
  
-   Office 2013, 32비트 또는 64비트 버전  
  
> [!WARNING]  
>  사용 중인 Excel 버전에 맞는 추가 기능 버전을 다운로드하십시오.  
  
 데이터 마이닝 추가 기능을 사용하려면 다음 SQL Server Analysis Services 버전 중 하나에 연결해야 합니다.  
  
-   Enterprise  
  
-   Business Intelligence  
  
-   Standard  
  
 연결하는 SQL Server Analysis Services의 버전에 따라 일부 고급 알고리즘을 사용하지 못할 수 있습니다. 자세한 내용은 [SQL Server 2014 버전에서 지원하는 기능](https://msdn.microsoft.com/library/cc645993.aspx)을 참조하십시오.  
  
 설치 관련 추가 도움말에 대 한 다운로드 센터에서이 페이지를 참조 하세요. [https://www.microsoft.com/download/details.aspx?id=29061](https://www.microsoft.com/download/details.aspx?id=29061)  
  
  
