---
title: 다차원 데이터 원본과 Power View 보고서 만들기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a34a67b5a963ba7c7adface2137a26e9194709d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-power-view-report-with-a-multidimensional-data-source"></a>다차원 데이터 원본이 포함된 파워 뷰 보고서 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  다차원 모델을 기반으로 파워 뷰 보고서를 만드는 것은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서나 Analysis Services 테이블 형식 모델을 기반으로 보고서를 만드는 것과 같습니다. 파워 뷰 보고서는 SharePoint 라이브러리의 보고서 데이터 원본 연결 파일(.rsds)에서 만들어집니다. .rsds를 만드는 방법에 대한 자세한 내용은 [Create a Report Data Source](../../analysis-services/multidimensional-models/create-a-report-data-source.md)를 참조하십시오.  
  
 시작하기 전에 다음을 알아야 합니다.  
  
-   다차원 모델에 대한 공유 보고서 데이터 원본 연결(.rsds)이 포함된 SharePoint 라이브러리의 이름과 위치.  
  
#### <a name="create-a-new-blank-power-view-report"></a>비어 있는 새 파워 뷰 보고서 만들기  
  
-   SharePoint 라이브러리에서 .rsds 공유 보고서 데이터 원본 연결(다차원 모델에 연결되는 .rsds) 옆의 화살표를 클릭한 다음 **파워 뷰 보고서 만들기**를 클릭합니다.  
  
  
