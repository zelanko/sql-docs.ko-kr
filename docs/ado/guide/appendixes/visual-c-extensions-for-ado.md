---
title: ADO의 visual c + + 확장 | Microsoft Docs
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
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350188"
---
# <a name="visual-c-extensions-for-ado"></a>ADO용 Visual C++ 확장
Visual c + + ADO 프로그래밍의 기본 메서드를 사용 하는 **#import** 지시문에 설명 된 대로 [Visual c + + ADO 프로그래밍 Microsoft](../../../ado/guide/appendixes/visual-c-ado-programming.md)합니다. 그러나 이전 버전의 ADO Visual c + +를 사용 하 여 프로그래밍 하는 대체 방법을와 함께 제공 되는: Visual c + + 확장 합니다. 이 섹션에서는 Visual c + + 확장 코드를 유지 관리 해야 하는 사람에 게이 기능을 설명 하지만 #을 사용 하 여 새 ADO 코드를 작성 해야**가져올**합니다.

 가장 작업 Visual c + + 프로그래머에 게 발생 하는 c + + 데이터 형식에 VARIANT 데이터 형식을 반환 하 고 클래스 또는 구조체에서 변환된 된 데이터를 저장 하는 데이터 변환는 ADO 사용 하 여 데이터를 검색 하는 경우 중 하나입니다. 번거로운 뿐만 VARIANT 데이터 형식을 통해 데이터를 c + + 검색 성능도 저하 시킵니다.

 ADO는 VARIANT를 거치지 않고 네이티브 C/c + + 데이터 형식으로 데이터 검색을 지 원하는 인터페이스를 제공 하 고 또한 인터페이스를 사용 하 여 단순화 하는 전처리기 매크로 제공 합니다. 결과 사용 하기 쉬우며 고 성능이 뛰어난 있는 유연한 도구입니다.

 일반적인 C/c + + 클라이언트 시나리오에서 레코드를 바인딩하는 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) C/c + + 구조체 또는 네이티브 C/c + + 형식을 포함 하는 클래스입니다. Variant를 통과 하는 경우 C/c + + 네이티브 형식으로 변형에서 변환 코드를 작성 해야 합니다. ADO의 Visual c + + 확장을 대상으로 Visual c + + 프로그래머에 대 한이 시나리오를 쉽게 수행 합니다.

 ADO의 Visual c + + 확장에 자세히 알아보려면 다음 항목을 참조 하세요.

-   [ADO의 Visual c + + 확장을 사용 하 여](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [Visual c + + 확장 예제를 사용 하 여 ADO](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>관련 항목
 [COM에 대 한 Visual c + + 구문 인덱스용 ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual c + + 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual c + + 확장을 사용 하 여](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual c + + 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)
