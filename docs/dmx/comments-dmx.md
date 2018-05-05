---
title: 주석 (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- comments [DMX]
- Data Mining Extensions [Analysis Services], comments
- double forward slashes
- commenting characters
- text strings [SQL Server]
- remarks [DMX]
- forward slash-asterisk character pairs
- DMX [Analysis Services], comments
- /*...*/ (comment)
- double hyphens
- // (comment)
- -- (comment character)
ms.assetid: 64d10eb5-4fe8-42c6-b387-eff336315e56
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5c4309b2b3aceb51ba17de90cdf33e62653da573
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="comments-dmx"></a>주석(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  확장 DMX (Data Mining) 주석은 프로그램에서 텍스트 문자열을 코드에 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 실행 되지 않습니다. 주석은 설명이라고도 합니다. 주석을 사용하여 코드에 대한 설명을 기록하거나 코드를 검사할 때 DMX 문 또는 스크립트 부분이 임시로 실행되지 않도록 할 수 있습니다.  
  
 주석을 사용하여 프로그램 코드에 대한 설명을 기록하면 나중에 더 편리하게 프로그램 코드를 유지 관리할 수 있습니다. 또한 주석을 사용하여 프로그램 이름, 코드를 작성한 개발자 이름 및 주요 코드를 변경한 날짜와 같은 정보를 기록하고 복잡한 계산이나 프로그래밍 메서드를 설명할 수 있습니다.  
  
 다음은 기본적인 주석 작성 지침입니다.  
  
-   주석에 영숫자나 기호를 사용할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 주석 안에 있는 모든 문자를 무시합니다.  
  
-   문 또는 스크립트 내에서 주석의 길이는 제한이 없습니다. 주석은 한 개 이상의 줄을 포함할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 다음과 같은 유형의 주석 문자를 지원합니다.  
  
-   **(이중 슬래시)입니다.** 이 주석 문자를 사용하여 실행 코드와 동일한 줄에 주석을 기록하거나 별도의 줄 전체에 주석을 기록할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 이중 슬래시부터 해당 줄의 끝 사이에 있는 모든 내용을 주석으로 처리합니다. 여러 줄에 걸쳐 주석을 기록하려면 각 주석 줄 앞에 이중 슬래시를 입력합니다. 이 주석 문자에 대 한 자세한 내용은 참조 [이중 슬래시 &#40;주석&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)합니다.  
  
-   **-(이중 하이픈).** 이 주석 문자를 사용하여 실행 코드와 동일한 줄에 주석을 기록하거나 별도의 줄 전체에 주석을 기록할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 이중 하이픈부터 해당 줄의 끝 사이에 있는 모든 내용을 주석으로 처리합니다. 여러 줄에 걸쳐 주석을 기록하려면 각 주석 줄 앞에 이중 하이픈을 입력합니다. 이 주석 문자에 대 한 자세한 내용은 참조 [- &#40;주석&#41; &#40;DMX&#41; 요약](../dmx/comment-dmx-summary.md)합니다.  
  
-   **/\* ... \*/ (슬래시-별표 문자 쌍).** 이 주석 문자를 사용하여 실행 코드와 동일한 줄에 주석을 기록하거나 별도의 줄 전체에 주석을 기록할 수 있고 실행 코드 안에도 주석을 기록할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 주석 문자에서 모든 내용을 (/ *)부터 닫는 주석 문자 (\*/)는 주석 처리 합니다. 주석이 여러 행을 만들려면 주석을 오픈 주석 문자 쌍과 함께 시작 (/\*), 닫는 주석 문자 쌍과 함께 주석을 끝냅니다 (\*/). 이 주석 줄에는 다른 주석 문자를 삽입해서는 안 됩니다. 이 주석 문자에 대 한 자세한 내용은 참조 [슬래시 별 &#40;주석&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions & #40; DMX & #41; 참조](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions & #40; DMX & #41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [일반 예측 함수 &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [구조 및 DMX 예측 쿼리 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
