---
title: ADO 용 Visual C++ 확장 | Microsoft Docs
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
ms.openlocfilehash: db11e86ab479ad0df4224d59c3408729fa9903ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926371"
---
# <a name="visual-c-extensions-for-ado"></a>ADO용 Visual C++ 확장
Visual C++를 사용 하 여 ADO를 프로그래밍 하는 기본 방법은 [Ado 프로그래밍 Microsoft Visual C++](../../../ado/guide/appendixes/visual-c-ado-programming.md)에서 설명한 대로 **#import** 지시어를 사용 하는 것입니다. 그러나 Visual C++를 사용 하 여 다른 프로그래밍 방법으로 제공 되는 이전 버전의 ADO에는 Visual C++ 확장이 있습니다. 이 섹션에서는 Visual C++ 확장 코드를 유지 관리 해야 하는 사용자를 위해이 기능을 설명 하지만 #**import**를 사용 하 여 새 ADO 코드를 작성 해야 합니다.

 ADO를 사용 하 여 데이터를 검색할 때 프로그래머가 직면 하는 가장 지루한 Visual C++ 작업 중 하나는 VARIANT 데이터 형식으로 반환 된 데이터를 c + + 데이터 형식으로 변환한 다음 변환 된 데이터를 클래스 또는 구조체에 저장 하는 것입니다. 복잡 하 게 하는 것 외에도 VARIANT 데이터 형식을 통해 c + + 데이터를 검색 하면 성능이 저하 됩니다.

 ADO는 변형을 거치지 않고 네이티브 C/c + + 데이터 형식으로 데이터를 검색할 수 있도록 지 원하는 인터페이스를 제공 하며, 인터페이스를 사용 하 여 간소화 하는 전처리기 매크로도 제공 합니다. 결과는 사용 하기 쉽고 성능이 뛰어난 유연한 도구입니다.

 일반적인 C/c + + 클라이언트 시나리오는 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 레코드를 c/c + + 구조체 또는 네이티브 c/c + + 형식을 포함 하는 클래스에 바인딩하는 것입니다. 변형 작업을 수행 하는 경우 VARIANT에서 C/c + + 네이티브 형식으로 변환 코드를 작성 해야 합니다. ADO의 Visual C++ 확장은 Visual C++ 프로그래머에 게이 시나리오를 훨씬 쉽게 만들 수 있도록 대상으로 합니다.

 ADO의 Visual C++ 확장에 대해 자세히 알아보려면 다음 항목을 참조 하세요.

-   [ADO 용 Visual C++ 확장 사용](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [Visual C++ 확장의 ADO 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>참고 항목
 COM [Visual C++ 확장](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md) 를 [사용 하는 Visual C++ 확장](../../../ado/guide/appendixes/using-visual-c-extensions.md) 예제 [에 대 한 Visual C++ 구문 인덱스에 대 한 ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md)
