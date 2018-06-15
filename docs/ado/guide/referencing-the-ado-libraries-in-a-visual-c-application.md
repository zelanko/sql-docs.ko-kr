---
title: Visual c + + 응용 프로그램에서 ADO 라이브러리 참조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a38e5df65def060668e60ee470dc379b873ab35
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273612"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Visual c + + 응용 프로그램에서 ADO 라이브러리 참조
Visual c + + 응용 프로그램에서 ADO의 최신 버전을 사용 하려면 다음을 사용 하 여 `#import` 지시문:  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 ADOX 또는 ADO MD를 사용 하려면 가져와야 *msadomd.dll* 또는 *msadox.dll*, 위의 구문을 사용 하 여 합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ADO의 이전 버전을 사용 하려면 대체 *msado15.dll* 위에 다음 형식 라이브러리 중 하나를 사용 합니다.  
  
-   *msado27.tlb*, ADO 2.7 Type Library  
  
-   *msado26.tlb*, ADO 2.6 Type Library  
  
-   *msado25.tlb*, ADO 2.5 형식 라이브러리  
  
-   *msado21.tlb*, ADO 2.1 형식 라이브러리  
  
-   *msado20.tlb*, ADO 2.0 형식 라이브러리
