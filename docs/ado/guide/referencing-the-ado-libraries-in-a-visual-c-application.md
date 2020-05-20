---
title: Visual C++ 응용 프로그램에서 ADO 라이브러리 참조 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a790ace40aa31324ce8b22127d8f6948ae86e059
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764764"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Visual C++ 애플리케이션에서 ADO 라이브러리 참조
Visual C++ 응용 프로그램에서 최신 버전의 ADO를 사용 하려면 다음 지시문을 사용 합니다 `#import` .  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 ADO MD 또는 ADOX를 사용 하려면 위의 구문을 사용 하 여 *msadomd* 또는 *msadox .dll*을 가져와야 합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 이전 버전의 ADO를 사용 하려면 위의 *msado15.dll* 을 다음 형식 라이브러리 중 하나로 바꿉니다.  
  
-   *msado27*, ADO 2.7 형식 라이브러리  
  
-   *msado26*, ADO 2.6 형식 라이브러리  
  
-   *msado25*, ADO 2.5 형식 라이브러리  
  
-   *msado21*, ADO 2.1 형식 라이브러리  
  
-   *msado20*, ADO 2.0 형식 라이브러리
