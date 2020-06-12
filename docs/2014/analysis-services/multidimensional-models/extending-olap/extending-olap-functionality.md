---
title: OLAP 기능 확장 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
author: minewiskan
ms.author: owend
ms.openlocfilehash: d64d1ac46e2571aa6f8065a8ea42e4cc43aa589e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546725"
---
# <a name="extending-olap-functionality"></a>OLAP 기능 확장
  프로그래머는 여러 데이터베이스 애플리케이션에서의 사용 및 용도 변경 기능을 제공하는 어셈블리, 개인 설정 확장 프로그램 및 저장 프로시저를 작성하여 Analysis Services를 확장할 수 있습니다. 어셈블리는 새 프로시저와 함수를 MDX 언어에 추가하거나 개인 설정 추가 기능을 사용하여 다차원 모델 기능을 확장하는 데 사용됩니다.  
  
 저장 프로시저를 사용하면 공통 코드를 한 번 개발하고 단일 위치에 저장할 수 있으므로 Analysis Services 데이터베이스 개발 및 구현을 간소화하여 외부 루틴을 호출할 수 있습니다. 또한 MDX의 기본 기능에서 제공하지 않는 비즈니스 기능을 애플리케이션에 추가할 수 있습니다.  
  
 개인 설정은 사용자마다 다른 동작을 제공하기 위해 큐브에 추가하는 사용자 지정 개체입니다. 개인 설정은 큐브에서 영구 개체는 아니지만 사용자 세션 중 클라이언트 애플리케이션에서 동적으로 적용되는 개체입니다. 예를 들어 데이터에 액세스하는 개인에 따라 통화 값의 통화를 변경하거나 개별화된 KPI를 제공하거나 온라인으로 구매하는 단골 고객에 대한 목표 제안 목록을 작성합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [개별화를 통해 OLAP 확장](extending-olap-through-personalizations.md)  
  
 [Analysis Services 개인 설정 확장 프로그램](analysis-services-personalization-extensions.md)  
  
 [저장 프로시저 정의](../../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
