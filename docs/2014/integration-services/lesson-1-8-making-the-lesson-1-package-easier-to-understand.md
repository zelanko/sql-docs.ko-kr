---
title: '8단계: 1단원 패키지를 쉽게 이해할 수 있도록 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e549018c7f0654ba40ddd486149059b37ddd46e9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072533"
---
# <a name="step-8-making-the-lesson-1-package-easier-to-understand"></a>8단계: 1단원 패키지를 쉽게 이해할 수 있도록 만들기
  1단원 패키지의 구성을 완료했으므로 이제 패키지 레이아웃을 정리하는 것이 좋습니다. 제어 및 데이터 흐름 레이아웃 셰이프의 크기가 제멋대로이거나 셰이프가 정렬 또는 그룹화되지 않은 경우 패키지의 기능을 이해하기가 매우 어려울 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools에서는 패키지 레이아웃의 서식을 쉽고 빠르게 지정할 수 있는 도구를 제공합니다. 서식 지정 기능에는 셰이프의 크기를 동일하게 지정하고 셰이프를 정렬하며 셰이프 간의 가로 및 세로 간격을 조정하는 기능이 포함됩니다.  
  
 패키지 기능에 대한 이해를 향상시킬 수 있는 다른 방법은 패키지 기능을 설명하는 주석을 추가하는 것입니다.  
  
 이 태스크에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools의 서식 지정 기능을 사용하여 데이터 흐름의 레이아웃을 개선하고 데이터 흐름에 주석도 추가합니다.  
  
### <a name="to-format-the-layout-of-the-data-flow"></a>데이터 흐름 레이아웃의 서식을 지정하려면  
  
1.  1단원 패키지를 아직 열지 않은 경우 솔루션 탐색기에서 Lesson 1.dtsx를 두 번 클릭합니다.  
  
2.  **데이터 흐름** 탭을 클릭합니다.  
  
3.  Extract Sample Currency 변환의 오른쪽 위에 커서를 놓고 클릭한 다음 데이터 흐름 구성 요소 전체를 포함하도록 커서를 끕니다.  
  
4.  **서식** 메뉴에서 **같은 크기로**를 가리킨 다음 **모두**를 클릭합니다.  
  
5.  데이터 흐름 개체를 선택한 경우에는 **서식** 메뉴에서 **맞춤**을 가리킨 다음 **왼쪽**을 클릭합니다.  
  
### <a name="to-add-an-annotation-to-the-data-flow"></a>데이터 흐름에 주석을 추가하려면  
  
1.  데이터 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 다음 **주석 추가**를 클릭합니다.  
  
2.  주석 상자에 다음 텍스트를 입력하거나 붙여 넣습니다.  
  
     **데이터 흐름이 파일에서 데이터를 추출하고 DimCurrency 테이블의 CurrencyKey 열과 DimDate 테이블의 DateKey 열에서 값을 조회한 다음 NewFactCurrencyRate 테이블에 데이터를 기록합니다.**  
  
     주석 상자에서 텍스트 줄을 바꾸려면 새로운 줄을 시작할 위치에 커서를 놓고 Enter 키를 누릅니다.  
  
     주석 상자에 텍스트를 추가하지 않은 경우 상자의 바깥쪽을 클릭하면 주석 상자가 사라집니다.  
  
## <a name="next-steps"></a>다음 단계  
 [9단계: 1단원 자습서 패키지 테스트](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
