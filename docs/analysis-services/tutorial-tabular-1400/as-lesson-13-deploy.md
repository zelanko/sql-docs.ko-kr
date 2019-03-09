---
title: 'Analysis Services 자습서 단원 13: 배포 | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ab561b096c4436349580201eec3b3ea10a8aaa75
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685310"
---
# <a name="deploy"></a>배포

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 배포 속성 구성 배포 하는 서버 및 모델에 대 한 이름을 지정 합니다. 다음 서버에 모델을 배포 합니다. 모델을 배포한 후에 보고 클라이언트 응용 프로그램을 사용 하 여 사용자를 연결할 수 합니다. 자세한 내용은 참조 하세요 [Azure Analysis Services에 배포](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) 하 고 [테이블 형식 모델 솔루션 배포](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)합니다.  
  
이 단원에 소요되는 예상 시간: **5 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원을 완료해야 합니다. [12 단원: Excel에서 분석](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)합니다.  

> [!IMPORTANT]  
> Azure Analysis Services에 배포 하는 경우이 있어야 합니다 [관리자 권한](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins) 는 serever에 있습니다.  

> [!IMPORTANT]  
> 온-프레미스 SQL server, AdventureWorksDW 예제 데이터베이스를 설치 하 고 Azure Analysis Services 서버에 모델을 배포 하는 경우는 [온-프레미스 데이터 게이트웨이](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) 필요 합니다.
  
## <a name="deploy-the-model"></a>모델 배포  
  
#### <a name="to-configure-deployment-properties"></a>배포 속성을 구성하려면  

  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **AW Internet Sales** 프로젝트를 마우스 클릭 **속성**합니다.  
  
2.  에 **AW Internet Sales 속성 페이지** 대화 상자의 **배포 서버**의 **Server** 속성을 전체 서버 이름을 입력 합니다. Azure Analysis Services에 연결 하는 경우 서버 이름에 전체 URL을 포함을 해야 합니다.

    ![as-lesson13-deploy-property](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  에 **데이터베이스** 속성에 입력 **Adventure Works Internet Sales**합니다.  
  
4.  에 **Model Name** 속성에 입력 **Adventure Works Internet Sales Model**합니다.  
  
5.  선택한 내용을 확인하고 **확인**을 클릭합니다.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Adventure Works Internet Sales를 배포 하려면
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **AW Internet Sales** 프로젝트 > **빌드**합니다.  

2.  마우스 오른쪽 단추로 클릭 합니다 **AW Internet Sales** 프로젝트 > **배포**합니다.

    Azure Analysis Services에 배포할 때 사용자 계정을 입력 하 라는 메시지가 표시 될 수 있습니다. 예를 들어 조직 계정과 암호를 입력 nancy@adventureworks.com합니다. 이 계정은 서버에서 관리자 여야 합니다.
  
    배포 대화 상자가 나타나고 메타 데이터 및 모델에 포함 된 각 테이블의 배포 상태를 표시 합니다.  
    
    ![as-lesson13-deploy-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. 배포가 성공적으로 완료되면 **닫기**를 클릭합니다.  
  

이 단원에서는 SSDT에서 테이블 형식 모델을 배포 하는 가장 일반적이 고 쉬운 메서드를 설명 합니다. 배포 마법사 또는 XMLA 및 AMO를 사용 하 여 자동화와 같은 고급 배포 옵션 유연성, 일관성 및 예약 된 배포를 제공 합니다. 자세한 내용은 참조 하세요 [테이블 형식 모델 솔루션 배포](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)합니다.

## <a name="conclusion"></a>결론  
축하합니다. 여러분이 작성 하 고 첫 번째 Analysis Services 테이블 형식 모델을 배포 했습니다. 이 자습서에서는 테이블 형식 모델을 만들기 위해 수행해야 하는 대부분의 일반적인 태스크를 완료하는 과정을 안내했습니다. 이제 Adventure Works Internet Sales Model이 배포되었으므로 SQL Server Management Studio를 사용하여 모델을 관리하고 처리 스크립트와 백업 계획을 만들 수 있습니다. 이제 사용자가 Microsoft Excel 또는 Power BI와 같은 보고 클라이언트 응용 프로그램을 사용 하 여 모델을 연결할 수 있습니다.  

![as-lesson13-ssms](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>다음 단계
[Power BI Desktop을 사용 하 여 연결](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[추가 단원-동적 보안](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[추가 단원-세부 정보 행](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[추가 단원-불규칙된 한 계층 구조](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
