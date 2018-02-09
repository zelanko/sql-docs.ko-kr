---
title: "Visual c + + 응용 프로그램에서 ADO 라이브러리 참조 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a554ff290c1ea3fa8ef5382e45fafbae5b1110d8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
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
  
-   *msado27.tlb*, ADO 2.7 Type Library  
  
-   *msado26.tlb*, ADO 2.6 Type Library  
  
-   *msado25.tlb*, ADO 2.5 Type Library  
  
-   *msado21.tlb*, ADO 2.1 Type Library  
  
-   *msado20.tlb*, ADO 2.0 Type Library
