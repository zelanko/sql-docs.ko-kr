---
title: Visual C++ ADO에 대 한 확장 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4432c125b0c860775911aa753984806a472a64ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864501"
---
# <a name="visual-c-extensions-for-ado"></a>ADO용 Visual C++ 확장
시각적 개체를 사용 하 여 ADO 프로그래밍의 기본 메서드를 C++ 을 사용 하는 **#import** 지시문에 설명 된 대로 [Microsoft Visual C++ ADO 프로그래밍](../../../ado/guide/appendixes/visual-c-ado-programming.md). 이전 버전의 ADO 시각적 개체를 사용 하 여 프로그래밍 하는 대체 방법을와 함께 제공 되는 반면 C++: 시각적 개체 C++ 확장 합니다. 이 섹션에서는 시각적 개체를 유지 해야 하는 사람에 게이 기능을 설명 C++ 확장 코드 이지만, 새 ADO 코드 써야 #을 사용 하 여**가져올**합니다.

 가장 작업 시각적 개체 중 하나가 C++ 프로그래머 얼굴 데이터 변환는 ADO 사용 하 여 데이터를 검색 하는 경우에 VARIANT 데이터 형식으로 반환을 C++ 데이터 형식 및 클래스 또는 구조체에서 변환된 된 데이터를 저장 합니다. 검색 될 뿐 아니라 번거로운, C++ VARIANT 데이터 형식을 통해 데이터 성능도 저하 시킵니다.

 네이티브 C에 데이터를 검색할 수 있도록 하는 인터페이스를 제공 하는 ADO /C++ 데이터는 VARIANT를 거치지 않고 형식 및 인터페이스를 사용 하 여 단순화 하는 전처리기 매크로 제공 합니다. 결과 사용 하기 쉬우며 고 성능이 뛰어난 있는 유연한 도구입니다.

 일반적인 C /C++ 의 레코드를 바인딩할 경우 클라이언트는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 는 c /C++ 구조체 또는 네이티브 C를 포함 하는 클래스 /C++ 형식. Variant를 통과 하는 경우 여기에 변형에서 C로 변환 코드를 작성 /C++ 기본 형식입니다. 시각적 개체 C++ 시각적 개체에 대 한이 시나리오를 쉽게 만드는 데 ADO에 대 한 확장으로 C++ 프로그래머입니다.

 시각적 개체에 자세히 알아보려면 다음 항목을 참조 C++ ADO에 대 한 확장입니다.

-   [시각적 개체를 사용 하 여 C++ ADO 확장](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [시각적 개체를 사용 하 여 ADO C++ 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>관련 항목
 [시각적 개체에 대 한 ADO C++ COM에 대 한 구문 인덱스](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [시각적 C++ 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md) [시각적 개체를 사용 하 여 C++ 확장](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)
