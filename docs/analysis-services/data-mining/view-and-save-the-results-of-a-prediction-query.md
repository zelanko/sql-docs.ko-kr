---
title: "예측 쿼리 결과 보기 및 저장 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "예측 쿼리 [Analysis Services]"
  - "예측 쿼리 결과 보기"
  - "예측 쿼리 결과 표시"
  - "마이닝 모델 예측 [Analysis Services], 결과 보기"
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 15
---
# 예측 쿼리 결과 보기 및 저장
  예측 쿼리 작성기를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 쿼리를 정의한 후에는 쿼리를 실행하고 쿼리 결과 보기로 전환하여 해당 결과를 확인할 수 있습니다.  
  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 정의하는 모든 데이터 원본의 테이블에 예측 쿼리 결과를 저장할 수 있습니다. 새 테이블을 만들거나 기존 테이블에 쿼리 결과를 저장할 수 있습니다. 기존 테이블에 결과를 저장할 경우 테이블에 현재 저장되어 있는 데이터를 덮어쓰도록 선택할 수 있습니다. 덮어쓰도록 선택하지 않으면 테이블의 기존 데이터에 쿼리 결과가 추가됩니다.  
  
### 쿼리 실행 및 결과 확인  
  
1.  **의 데이터 마이닝 디자이너에 있는** 마이닝 모델 예측 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭의 도구 모음에서 **결과** 를 클릭합니다.  
  
     쿼리 결과 보기가 열리고 쿼리가 실행됩니다. 쿼리 결과가 뷰어에 표로 표시됩니다.  
  
### 테이블에 예측 쿼리 결과 저장  
  
1.  데이터 마이닝 디자이너에 있는 **마이닝 모델 예측** 탭의 도구 모음에서 **쿼리 결과 저장**을 클릭합니다.  
  
     **데이터 마이닝 쿼리 결과 저장** 대화 상자가 열립니다.  
  
2.  **데이터 원본** 목록에서 데이터 원본을 선택하거나 **새로 만들기** 를 클릭하여 새 데이터 원본을 만듭니다.  
  
3.  **테이블 이름** 입력란에 테이블 이름을 입력합니다. 이미 테이블이 있을 경우 테이블 내용을 쿼리 결과로 바꾸려면 **기존 항목 덮어쓰기** 를 선택합니다. 테이블 내용을 덮어쓰지 않으려면 이 확인란을 선택하지 마십시오. 그러면 테이블의 기존 데이터에 새 쿼리 결과가 추가됩니다.  
  
4.  데이터 원본 뷰에 테이블을 추가하려면 **DSV에 추가** 에서 데이터 원본 뷰를 선택합니다.  
  
5.  **저장**을 클릭합니다.  
  
    > [!WARNING]  
    >  대상이 계층적 행 집합을 지원하지 않는 경우 FALTTENED 키워드를 결과에 추가하여 플랫 테이블로 저장할 수 있습니다.  
  
  