---
title: "8 단원: 동작 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: 15459396-83c9-48a0-b10a-99ae38768c79
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 556766b328f7af4086643235f126ea3c5a459332
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-8-defining-actions"></a>8단원: 동작 정의
이 단원에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트에 동작을 정의하는 방법을 알아봅니다. 동작은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에 저장되며 클라이언트 응용 프로그램에 통합되고 사용자가 시작할 수 있는 MDX(Multidimensional Expressions) 문입니다.  
  
> [!NOTE]  
> 이 자습서의 모든 단원에 대한 완료된 프로젝트를 온라인으로 사용할 수 있습니다. 이전 단원에서 완료된 프로젝트를 시작 지점으로 사용하여 어떠한 단원으로든 이동할 수 있습니다. 이 자습서와 함께 제공되는 샘플 프로젝트를 다운로드하려면[여기를 클릭](http://go.microsoft.com/fwlink/?LinkID=221866) 하십시오.  
  
[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 다음 표에 설명된 동작 유형을 지원합니다.  
  
|||  
|-|-|  
|명령줄|명령 프롬프트에서 명령을 실행합니다.|  
|데이터 집합|데이터 집합을 클라이언트 응용 프로그램으로 반환합니다.|  
|드릴스루|행 집합을 반환하기 위해 클라이언트가 실행하는 드릴스루 문을 식으로 반환합니다.|  
|Html|인터넷 브라우저에서 HTML 스크립트를 실행합니다.|  
|소유|이 표에 나열되지 않은 인터페이스를 사용하여 작업을 수행합니다.|  
|보고서|매개 변수가 있는 URL 기반 요청을 보고서 서버로 전송하고 보고서를 클라이언트 응용 프로그램으로 반환합니다.|  
|행 집합|행 집합을 클라이언트 응용 프로그램으로 반환합니다.|  
|문|OLE DB 명령을 실행합니다.|  
|URL|동적 웹 페이지를 인터넷 브라우저로 표시합니다.|  
  
동작을 사용하여 응용 프로그램을 시작하거나 선택한 항목의 컨텍스트 내에서 다른 작업을 수행할 수 있습니다. 자세한 내용은 [동작&#40;Analysis Services - 다차원 데이터&#41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)및 [다차원 모델의 동작](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
> [!NOTE]  
> 동작의 예는 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 예제 데이터 웨어하우스에 있는 예나 계산 도구 창의 템플릿 탭에 있는 동작 예를 참조하십시오. 이 데이터베이스를 설치하는 방법에 대한 자세한 내용은 [Analysis Services 다차원 모델링 자습서에 사용할 샘플 데이터 및 프로젝트 설치](../analysis-services/install-sample-data-and-projects.md)를 참조하세요.  
  
이 단원에서는 다음 태스크를 다룹니다.  
  
[드릴스루 동작 정의 및 사용](../analysis-services/lesson-8-1-defining-and-using-a-drillthrough-action.md)  
이 태스크에서는 자습서 앞부분에서 정의한 팩트 차원 관계를 통해 드릴스루 동작을 정의, 사용 및 수정합니다.  
  
## <a name="next-lesson"></a>다음 단원  
[9단원: 큐브 뷰 및 번역 정의](../analysis-services/lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>참고 항목  
[Analysis Services Tutorial 시나리오](../analysis-services/analysis-services-tutorial-scenario.md)  
[다차원 모델링&#40;Adventure Works 자습서&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
[동작&#40;Analysis Services - 다차원 데이터&#41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)  
[다차원 모델의 동작](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
  
  
