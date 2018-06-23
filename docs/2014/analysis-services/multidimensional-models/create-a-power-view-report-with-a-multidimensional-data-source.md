---
title: 다차원 데이터 원본과 Power View 보고서 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b9b6f4c9-7e1f-4f61-b657-8986e39a6af2
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 736048d9cb6c8c2054c9d86bd3c8a8a0e2411daf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080727"
---
# <a name="create-a-power-view-report-with-a-multidimensional-data-source"></a>다차원 데이터 원본이 포함된 파워 뷰 보고서 만들기
  다차원 모델을 기반으로 Power View 보고서를 만드는 것은 PowerPivot 통합 문서나 Analysis Services 테이블 형식 모델을 기반으로 보고서를 만드는 것과 같습니다. Power View 보고서는 SharePoint 라이브러리의 보고서 데이터 원본 연결 파일(.rsds)에서 만들어집니다. .rsds를 만드는 방법에 대한 자세한 내용은 [Create a Report Data Source](create-a-report-data-source.md)를 참조하십시오.  
  
 시작하기 전에 다음을 알아야 합니다.  
  
-   다차원 모델에 대한 공유 보고서 데이터 원본 연결(.rsds)이 포함된 SharePoint 라이브러리의 이름과 위치.  
  
#### <a name="create-a-new-blank-power-view-report"></a>비어 있는 새 파워 뷰 보고서 만들기  
  
-   SharePoint 라이브러리에서 .rsds 공유 보고서 데이터 원본 연결(다차원 모델에 연결되는 .rsds) 옆의 화살표를 클릭한 다음 **파워 뷰 보고서 만들기**를 클릭합니다.  
  
  