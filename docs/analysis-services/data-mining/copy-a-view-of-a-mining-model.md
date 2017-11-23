---
title: "마이닝 모델의 뷰 복사 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clipboards [data mining]
- Mining Model Viewer [Analysis Services], clipboards
- copying mining models to clipboard
ms.assetid: 768372db-e5b4-4990-b459-03d854fd9a6d
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 77e2e0228532d7a0ef9c379200ef063fc84b8430
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="copy-a-view-of-a-mining-model"></a>마이닝 모델의 뷰 복사
  **데이터 마이닝 디자이너의** 마이닝 모델 뷰어 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 탭에서는 마이닝 모델 유형마다 별도의 뷰어가 사용됩니다. 이 중 몇몇 뷰어에는 내용을 클립보드로 복사하고 문서나 이미지 조작 소프트웨어에 붙여넣을 수 있는 구성 요소가 있습니다. 다음 구성 요소에서 이 기능을 사용할 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터 뷰어와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 클러스터 뷰어의 클러스터 다이어그램  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 뷰어와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 트리 뷰어의 의사 결정 트리  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시퀀스 클러스터 뷰어의 상태 전환  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 트리 뷰어, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 뷰어 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 연결 규칙 뷰어의 종속성 네트워크  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 일반 콘텐츠 트리 뷰어의 Node Details 창의 마이닝 모델 콘텐츠  
  
 전체 마이닝 모델 표현을 복사하거나 뷰어에 표시할 일부만 복사할 수 있습니다.  
  
> [!WARNING]  
>  뷰어를 사용하여 모델을 복사할 경우 새 모델 개체가 만들어지지 않습니다. 새 모델을 만들려면 마법사 또는 데이터 마이닝 디자이너를 사용해야 합니다. 자세한 내용은 [마이닝 모델 복사본 만들기](../../analysis-services/data-mining/make-a-copy-of-a-mining-model.md)를 참조하세요.  
  
### <a name="to-copy-the-complete-model-to-the-clipboard"></a>전체 모델을 클립보드로 복사하려면  
  
1.  **마이닝 모델 뷰어** 탭의 **마이닝 모델** 목록에서 보려는 마이닝 모델을 선택합니다.  
  
2.  **종속성 네트워크** 등의 적절한 탭을 선택하고 해당 탭의 도구 모음에서 **전체 그래프 복사** 를 클릭합니다.  
  
### <a name="to-copy-the-visible-piece-of-the-model-to-the-clipboard"></a>모델의 표시되는 부분을 클립보드로 복사하려면  
  
1.  **마이닝 모델 뷰어** 탭의 **마이닝 모델** 목록에서 보려는 마이닝 모델을 선택합니다.  
  
2.  **종속성 네트워크** 등의 적절한 탭을 선택하고 확대 또는 축소하여 원하는 수준으로 모델을 표시합니다.  
  
3.  선택한 탭의 도구 모음에서 **그래프 뷰 복사** 를 클릭합니다.  
  
### <a name="to-copy-the-mining-model-content-to-the-clipboard"></a>마이닝 모델 콘텐츠를 클립보드로 복사하려면  
  
1.  **마이닝 모델 뷰어** 탭의 **마이닝 모델** 목록에서 보려는 마이닝 모델을 선택합니다.  
  
2.  **뷰어** 드롭다운 목록에서 **Microsoft 일반 콘텐츠 트리 뷰어**를 선택합니다.  
  
3.  **노드 캡션(고유 ID)** 창에서 노드를 클릭합니다.  
  
4.  **노드 정보** 창을 마우스 오른쪽 단추로 클릭한 다음 **모두 선택**을 선택합니다.  
  
5.  **노드 정보** 창을 마우스 오른쪽 단추로 다시 클릭한 다음 **복사**를 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
