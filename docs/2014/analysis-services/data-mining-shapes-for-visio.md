---
title: Visio 용 데이터 마이닝 셰이프 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92630f90d7b18ad668dcffc02feeb65990cf3c84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689989"
---
# <a name="data-mining-shapes-for-visio"></a>Visio용 데이터 마이닝 셰이프
  Visio용 데이터 마이닝 셰이프는 데이터 마이닝 모델을 표시하기 위해 사용자 지정된 템플릿을 제공합니다. 이러한 템플릿을 사용하여, 사용자가 만든 모델에 연결할 수 있으며 데이터 마이닝의 결과를 보여 주기 위한 대화형 프레젠테이션을 만들 수 있습니다.  
  
 템플릿은 정적 그래프에 비해 많은 이점을 제공 하 고 화면 캡처-Analysis Services 인스턴스에 저장 되는 기본 데이터 마이닝 모델과 상호 작용 하며 마이닝 모델에서 패턴이 표시 되는 방식을 사용자 지정할 수 있습니다. 트리 모델을 축소 및 확장하고 데이터 노드 또는 특성별로 필터링하며 확률 및 계수와 같은 모델 통계를 표시할 수 있습니다.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Visio 템플릿에는 다음과 같은 마법사가 포함되어 있습니다.  
  
-   **종속성 네트워크 다이어그램:** 의사 결정 트리와 신경망에 대 한 그래프를 만들려면이 마법사를 사용 합니다.  
  
-   **의사 결정 트리 다이어그램:** 이 마법사를 사용 하 여 의사 결정 지점 및 의사 결정 트리 모델을 사용 하 여 연결 하는 수식을 보여 주는 다이어그램을 만듭니다. 이 다이어그램은 회귀 모델에서도 사용할 수 있습니다.  
  
-   **클러스터 다이어그램:** 조각화 모델에 대해 색상이 지정 된 그래프를 만들려면이 마법사를 사용 합니다. 특성 판별, 클러스터 프로필 및 종속성과 같은 뷰 사이를 전환하고 클러스터의 모양을 사용자 지정할 수 있습니다.  
  
## <a name="installation"></a>설치  
 기본적으로 Visio 용 데이터 마이닝 템플릿을 설치할 때에 다음 파일이 설치 됩니다 \<드라이브 > files\microsoft SQL Server 2012 DM Add-ins (또는 \<드라이브 > \ 또는 Program Files (x86) \Microsoft SQL Server 2012 DM Add-Ins):  
  
-   **Microsoft Data Mining.vst** 미리 정의 된 서식, 레이아웃 및 데이터 마이닝 셰이프를 사용 하 여 사용할 수 있도록 마법사가이 템플릿에 포함 되어 있습니다.  
  
-   **Microsoft Data Mining Shape Studio.vss** 이 스텐실 파일 템플릿과 사용 하 여 연결 된 셰이프를 포함 합니다.  
  
## <a name="how-to-use-the-templates"></a>템플릿 사용 방법  
 템플릿을 열려면 셰이프 파일을 두 번 클릭하거나 Visio를 연 다음 셰이프 템플릿을 엽니다.  
  
1.  스텐실에서 Visio 데이터 마이닝 셰이프 중 하나를 새 페이지에 끌어서 놓습니다.  
  
2.  마법사가 시작되면 표시하려는 데이터 마이닝 모델이 있는 서버에 연결합니다.  
  
3.  시각화 유형과 모델 유형이 일치하는 데이터 마이닝 모델을 선택합니다.  
  
4.  데이터를 표시하고 포맷하는 방법에 대한 옵션을 설정합니다.  
  
5.  완료 한 후 합니다 **데이터 마이닝 셰이프 마법사**, 수정 하 고 Visio의 기능을 사용 하 여 향상 시킬 수 있는 다이어그램을 사용 해야 합니다.  
  
 작업 및 Visio 모델 다이어그램을 향상 하는 방법에 대 한 자세한 내용은 참조 하세요. [보기 데이터 마이닝 Visio에서 모델 &#40;데이터 마이닝 추가 기능&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>요구 사항  
  
-   템플릿을 사용하려면 먼저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결해야 합니다.  
  
     마법사는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버를 선택하고 마이닝 모델이 포함된 데이터베이스를 지정하라는 메시지를 표시합니다.  
  
     연결을 만드는 방법에 대 한 자세한 내용은 [원본 데이터에 연결 &#40;Excel 용 데이터 마이닝 클라이언트&#41;](connect-to-source-data-data-mining-client-for-excel.md)합니다.  
  
-   테이블 분석 도구를 사용하는 경우 모델을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버에 저장해야 하며 임시 모델을 사용하지 않아야 합니다.  
  
-   모델을 만든 것 이어야 지원 되는 알고리즘 중 하나를 사용 하 여: 클러스터링, 의사 결정 트리, 신경망, 원시 Bayes 또는 로지스틱 회귀 분석 합니다.  
  
  
