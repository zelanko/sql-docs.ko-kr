---
title: Visual c + +에서 오류 처리 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e33d28201e1a2e4f7df8ac330ac89b3f00194b14
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630671"
---
# <a name="handling-errors-in-visual-c"></a>Visual C++로 오류 처리
Com에서 대부분의 작업 함수를 성공적으로 완료 되었는지 여부를 나타내는 HRESULT 반환 코드를 반환 합니다. #Import 지시문 각 "원시" 메서드 또는 속성 래퍼 코드를 생성 하 고 반환된 된 HRESULT를 확인 합니다. HRESULT 오류를 나타냅니다 래퍼 코드는 인수로 서 COM 오류를 HRESULT 반환 코드를 사용 하 여 호출 _com_issue_errorex()에서 throw 합니다. COM 오류 개체를 낼 수 있습니다는 **try / catch** 블록입니다. (효율성의 위해서 catch _com_error 개체에 대 한 참조.)  
  
 ADO 오류입니다: ADO 작업이 실패에서 하 여 발생 합니다. 기본 공급자에서 반환한 오류를 표시 **오류** 개체를 **연결** 개체의 **오류** 컬렉션입니다.  
  
 만 #import 지시문 메서드 및 ADO.dll에 선언 된 속성에 대 한 오류 처리 루틴을 만듭니다. 그러나 사용자 고유의 오류 검사 매크로 또는 인라인 함수를 작성 하 여는 동일한이 오류 처리 메커니즘을 활용을 걸릴 수 있습니다. 예제 C++® 확장 항목을 참조 하십시오.
