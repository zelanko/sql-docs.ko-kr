---
title: 시각적 개체에서 ADO 라이브러리 참조 C++ 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 772dbc55fdeb3b038399a3740be472497666e4da
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222029"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Visual C++ 애플리케이션에서 ADO 라이브러리 참조
시각적 개체에서 최신 버전의 ADO 사용 하려면 C++ 응용 프로그램에 다음 사용 하 여 `#import` 지시문:  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 ADOX 또는 ADO MD를 사용 하려면 가져와야 *msadomd.dll* 하거나 *msadox.dll*, 위의 구문을 사용 하 여 합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 이전 버전의 ADO 사용 하려면 대체 *msado15.dll* 위에 다음 형식 라이브러리 중 하나를 사용 하 여 합니다.  
  
-   *msado27.tlb*, ADO 2.7 Type Library  
  
-   *msado26.tlb*, ADO 2.6 Type Library  
  
-   *msado25.tlb*, ADO 2.5 형식 라이브러리  
  
-   *msado21.tlb*, ADO 2.1 형식 라이브러리  
  
-   *msado20.tlb*, ADO 2.0 형식 라이브러리
