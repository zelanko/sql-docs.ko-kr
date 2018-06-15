---
title: ADO에 대 한 visual c + + 확장 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c9200939a34f3d1a2af936388acaa6740387416
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270552"
---
# <a name="visual-c-extensions"></a>Visual c + + 확장
Visual c + +를 사용 하 여 ADO를 프로그래밍 하는 기본 방법은 사용 하는 **#import** 지시문에 설명 된 대로 [Visual c + + ADO 프로그래밍 Microsoft](../../../ado/guide/appendixes/visual-c-ado-programming.md)합니다. ADO의 이전 버전의 Visual c + +를 사용 하는 프로그래밍 방법도와 함께 제공 되는 반면: Visual c + + 확장 합니다. 이 섹션에서는 Visual c + + 확장 코드를 유지 관리 해야 하는 사람에 게이 기능을 문서화 하지만 #을 사용 하 여 새 ADO 코드 작성**가져올**합니다.

 가장 작업 Visual c + + 프로그래머 면 ADO 사용 하 여 데이터를 검색 하는 클래스 또는 구조체에 변환된 된 데이터를 저장 하는 c + + 데이터 형식에는 VARIANT 데이터 형식으로 반환 된 데이터 변환 하는 경우 중 하나입니다. 번거로운 않도록, VARIANT 데이터 형식을 통해 데이터를 c + + 검색 성능도 저하 시킵니다.

 ADO는 데이터를 검색할 수 네이티브 C/c + + 데이터 형식을 VARIANT를 통하지 않고는 인터페이스를 제공 하 고 또한 인터페이스를 사용 하 여 단순화 하는 전처리기 매크로 제공 합니다. 결과 뛰어난 성능을 쉽게 사용할 수 있으며 유연한 도구입니다.

 일반적인 C/c + + 클라이언트 시나리오에서 레코드를 바인딩하는 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) C/c + + 구조체 또는 네이티브 C/c + + 형식이 포함 된 클래스에 있습니다. Variant를 통과 하는 경우이 VARIANT에서 C/c + + 네이티브 형식으로 변환 코드를 작성 해야 합니다. Visual c + + 프로그래머에 대 한이 시나리오를 훨씬 쉽게 만드는 데 ADO에 대 한 Visual c + + 확장명 대상입니다.

 ADO에 대 한 Visual c + + 확장에 대 한 자세한 내용을 보려면 다음 항목을 참조 하십시오.

-   [Visual c + + 확장을 사용 하 여 ADO에 대 한](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [Visual c + + 확장 예제를 사용 하 여 ADO](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>관련 항목
 [Visual c + + 구문 인덱스에 대 한 COM ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual c + + 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual c + + 확장을 사용 하 여](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual c + + 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)
