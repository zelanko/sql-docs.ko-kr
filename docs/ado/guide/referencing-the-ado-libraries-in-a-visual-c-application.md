---
title: "Visual c + + 응용 프로그램에서 ADO 라이브러리 참조 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.prod: sql-non-specified
ms.technology: "“drivers”"
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 44d731d8c9e61c29f1dc9eb0c8ea12d57402639c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Visual c + + 응용 프로그램에서 ADO 라이브러리 참조
Visual c + + 응용 프로그램에서 ADO의 최신 버전을 사용 하려면 다음을 사용 하 여 `#import` 지시문:  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 ADOX 또는 ADO MD를 사용 하려면 가져와야 *msadomd.dll* 또는 *msadox.dll*, 위의 구문을 사용 하 여 합니다.  
  
## <a name="backward-compatibility"></a>이전 버전과의 호환성  
 ADO의 이전 버전을 사용 하려면 대체 *msado15.dll* 위에 다음 형식 라이브러리 중 하나를 사용 합니다.  
  
-   *msado27.tlb*, ADO 2.7 형식 라이브러리  
  
-   *msado26.tlb*, ADO 2.6 형식 라이브러리  
  
-   *msado25.tlb*, ADO 2.5 형식 라이브러리  
  
-   *msado21.tlb*, ADO 2.1 형식 라이브러리  
  
-   *msado20.tlb*, ADO 2.0 형식 라이브러리

