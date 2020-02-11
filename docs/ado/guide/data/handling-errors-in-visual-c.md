---
title: Visual C++에서 오류 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb9eb29a78c3ec5f47e3ff09641ba04ca01d204a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925121"
---
# <a name="handling-errors-in-visual-c"></a>Visual C++로 오류 처리
COM에서 대부분의 작업은 함수가 성공적으로 완료 되었는지 여부를 나타내는 HRESULT 반환 코드를 반환 합니다. #Import 지시문은 각 "raw" 메서드 또는 속성에 대 한 래퍼 코드를 생성 하 고 반환 된 HRESULT를 확인 합니다. HRESULT가 실패를 나타내면 래퍼 코드는 HRESULT 반환 코드를 인수로 사용 하 여 _com_issue_errorex ()를 호출 하 여 COM 오류를 throw 합니다. COM 오류 **개체는 try-catch 블록에서** catch 할 수 있습니다. 효율성을 높이기 위해 _com_error 개체에 대 한 참조를 catch 합니다.  
  
 Ado 오류가 발생 하 여 ado 작업이 실패 하는 것을 명심 해야 합니다. 기본 공급자가 반환 하는 오류는 **연결** 개체의 **Errors** 컬렉션에서 **오류** 개체로 표시 됩니다.  
  
 #Import 지시문은 ADO .dll에 선언 된 메서드 및 속성에 대 한 오류 처리 루틴을 만듭니다. 그러나 사용자 고유의 오류 검사 매크로나 인라인 함수를 작성 하 여 이와 동일한 오류 처리 메커니즘을 활용할 수 있습니다. 예제는® 확장 Visual C++ 항목을 참조 하세요.
