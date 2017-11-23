---
title: "14 단원: 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: efcf6f3c540325b07c5e8b5a3892f2ed464141f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-13-deploy"></a>13단원: 배포
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 배포 속성 구성 온-프레미스 또는 Azure 서버 인스턴스 및 모델에 대 한 이름을 지정합니다. 그런 다음 해당 인스턴스에 모델을 배포 합니다. 모델 배포 된 후 사용자가 연결할 수는 보고 클라이언트 응용 프로그램을 사용 하 여 합니다. 배포에 대 한 자세한 참조 [테이블 형식 모델 솔루션 배포](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md) 및 [Azure Analysis Services에 배포](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)합니다.  
  
이 단원에 소요되는 예상 시간: **5분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [12 단원: Excel에서 분석](../analysis-services/lesson-12-analyze-in-excel.md)합니다.  
  
## <a name="deploy-the-model"></a>모델 배포  
  
#### <a name="to-configure-deployment-properties"></a>배포 속성을 구성하려면  
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **AW Internet Sales** 프로젝트를 마우스 클릭 **속성**합니다.  
  
2.  에 **AW Internet Sales 속성 페이지** 대화 상자의 **배포 서버**에 **서버** 속성을 Azure Analysis Services 서버 이름을 입력 또는 테이블 형식 모드에서 실행 되는 온-프레미스 서버 인스턴스. 모델에 배포 될 서버 인스턴스가 될 수 있습니다.  

    ![aas-배포-배포-서버-속성](../analysis-services/media/aas-deploy-deployment-server-property.png)
 
    > [!IMPORTANT]  
    > 원격 Analysis Services 인스턴스에서 순서를 배포 하려면에 대 한 관리자 권한이 있어야 합니다.  
  
3.  에 **데이터베이스** 속성을 입력 **Adventure Works Internet Sales**합니다.  
  
4.  에 **모델 이름** 속성을 입력 **Adventure Works Internet Sales Model**합니다.  
  
5.  선택한 내용을 확인하고 **확인**을 클릭합니다.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Adventure Works Internet Sales 테이블 형식 모델을 배포하려면  
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **AW Internet Sales** 프로젝트 > **빌드**합니다.  

2.  마우스 오른쪽 단추로 클릭는 **AW Internet Sales** 프로젝트 > **배포**합니다.

    Azure Analysis Services를 배포할 때는 사용자 계정을 입력 하 라는 메시지가 표시 될 가능성이 합니다. 예를 들어 조직의 계정 및 passsword, 입력 nancy@adventureworks.com합니다. 이 계정은 관리자에 서버 인스턴스에 있어야 합니다.
  
    배포 대화 상자가 나타나고 메타데이터 및 모델에 포함된 각 테이블의 배포 상태가 표시됩니다.  
    
    ![aas 배포 상태](../analysis-services/media/aas-deploy-status.png)
  
3. 배포가 성공적으로 완료되면 **닫기**를 클릭합니다.  
  
## <a name="conclusion"></a>결론  
축하합니다. 제작 및 첫 번째 Analysis Services 테이블 형식 모델을 배포할 마쳤습니다. 이 자습서에서는 테이블 형식 모델을 만들기 위해 수행해야 하는 대부분의 일반적인 태스크를 완료하는 과정을 안내했습니다. 이제 Adventure Works Internet Sales Model이 배포되었으므로 SQL Server Management Studio를 사용하여 모델을 관리하고 처리 스크립트와 백업 계획을 만들 수 있습니다. 사용자 수 또한 이제 Microsoft Excel 또는 Power BI와 같은 보고 클라이언트 응용 프로그램을 사용 하 여 모델에 연결 됩니다.  

![로-테이블 형식-lesson13-ssms](../analysis-services/media/as-tabular-lesson13-ssms.png)
  
  
## <a name="see-also"></a>참고 항목  
[DirectQuery 모드&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[기본 데이터 모델링 및 배포 속성 구성&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[테이블 형식 model 데이터베이스&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  ## <a name="whats-next"></a>다음 단계
*  [추가 단원-행 필터를 사용 하 여 동적 보안 구현](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)합니다.

*  [추가 단원-Power View 보고서에 대 한 보고 속성 구성](../analysis-services/supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)합니다.
