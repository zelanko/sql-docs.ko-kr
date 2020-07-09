---
title: '8단계: 1단원 패키지 주석 달기 및 형식 | Microsoft Docs'
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fffa5eed608e8cd3faeb13b084e15554e4a8092f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729407"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>1-8단원: 1단원 패키지 주석 달기 및 형식 

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이제 1단원 패키지의 구성을 완료했으므로 패키지 레이아웃을 정리해야 할 때입니다. 제어 흐름과 데이터 흐름 레이아웃의 모양이 다른 크기이거나 균등하지 않은 경우 패키지를 이해하기가 더 어려울 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools는 패키지 레이아웃을 쉽게 서식 지정하는 도구를 제공합니다. 서식 지정 기능에는 세이프를 같은 크기로 만들고 셰이프를 정렬하며 셰이프 간의 가로 및 세로 간격을 조정하는 기능이 포함됩니다.  
  
패키지 기능에 대한 이해를 향상시킬 수 있는 다른 방법은 패키지 기능을 설명하는 주석을 추가하는 것입니다.  
  
이 태스크에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools의 서식 지정 기능을 사용하여 데이터 흐름의 레이아웃을 개선하고 주석도 추가합니다.  
  
## <a name="format-the-layout-of-the-data-flow"></a>데이터 흐름 레이아웃 서식 지정  
  
1.  1단원 패키지를 아직 열지 않은 경우 **솔루션 탐색기**에서 **Lesson 1.dtsx를** 두 번 클릭합니다.  
  
2.  **데이터 흐름** 탭을 선택합니다.  
  
3.  모든 데이터 흐름 구성 요소를 한 번에 선택하려면 **편집** > **모두 선택**을 사용합니다.
  
4.  **서식** 메뉴에서 **크기 같게 만들기**를 선택한 다음, **둘 다**를 선택합니다.  
  
5.  데이터 흐름 개체를 선택한 경우에는 **서식** 메뉴에서 **맞춤**을 선택한 다음, **센터**를 선택합니다.  

6.  데이터 흐름 개체를 선택한 경우에는 **서식** 메뉴에서 **세로 간격**을 가리킨 다음, **같게 만들기**를 선택합니다.  
  
## <a name="add-an-annotation-to-the-data-flow"></a>데이터 흐름에 주석 추가  
  
1.  데이터 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 다음, **주석 추가**를 선택합니다.  
  
2.  주석 상자에 다음 텍스트를 입력하거나 붙여넣습니다.  
  
    데이터 흐름이 파일에서 데이터를 추출하고 DimCurrency 테이블의 CurrencyKey 열과 DimDate 테이블의 DateKey 열에서 값을 조회한 다음 NewFactCurrencyRate 테이블에 데이터를 기록합니다.
  
    주석 상자에서 텍스트 줄을 바꾸려면 새로운 줄을 시작할 위치에 커서를 놓고 **Enter**를 누릅니다.  
  
    주석 상자에 텍스트를 추가하지 않은 경우 상자의 바깥쪽을 클릭하면 상자가 사라집니다.  이 동작 때문에, 주석 상자에 텍스트를 붙여넣으려면 주석 추가를 선택하기 전에 텍스트를 클립보드에 복사합니다. 
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[9단계: 1단원 패키지 테스트](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
