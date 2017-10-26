---
title: "맞춤 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 412c04f8181997738bac1fc7b457c9ec0c3efcde
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="alignment"></a>맞춤
ODBC 응용 프로그램의 맞춤 문제는 일반적으로 서로 다른 응용 프로그램에 보다 합니다. 즉, 대부분의 ODBC 응용 프로그램 문제가 없거나 거의 맞춤. 주소 정렬 되어 있지 않기에 의해 엄격히 규제 되어 하드웨어 및 운영 체제와 다르며 성능이 약간 저하 같은 사소한 문제로 또는 런타임 오류로 같이 주요 될 수 있습니다. 따라서 ODBC 응용 프로그램 및 휴대용 ODBC 응용 프로그램, 특히 주의 해야 데이터를 제대로 정렬 합니다.  
  
 하나는 큰 메모리 블록 할당 하 고 해당 메모리의 다른 부분 결과 집합의 열에 바인딩할 때 ODBC 응용 프로그램 맞춤 문제가 발생 하는 경우의 예는 합니다. 이 일반 응용 프로그램 실행 시 결과 집합의 모양을 결정 하 고 할당 하 고 해야 그에 따라 메모리를 바인딩할 때 발생할 가능성이 가장 높습니다.  
  
 예를 들어, 응용 프로그램을 실행 한 **선택** 문은 사용자가 입력 하 고이 문의 결과 인출 합니다. 이 결과 집합의 모양이 프로그램이 작성 된 경우 알려지지 않은 때문에 응용 프로그램 결과 집합을 만든 후 각 열의 유형을 확인 하 고 그에 따라 메모리를 바인딩할 해야 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 하는 큰 메모리 블록 할당 하 고 각 열에 해당 블록에서 다른 주소를 바인딩합니다. 열에 있는 데이터에 액세스 하려면 응용 프로그램에는 해당 열에 바인딩된 메모리를 캐스팅 합니다.  
  
 다음 다이어그램은 설정 하 고 각 SQL 데이터 형식에 대 한 기본 C 데이터 형식을 사용 하 여 메모리 블록을 바인딩하여 어떻게 샘플 결과 보여줍니다. 각 "X"는 단일 바이트를의 메모리를 나타냅니다. (이 예에서는 열에 바인딩된 데이터 버퍼를 표시 하는 데 사용 합니다. 이 편의상 수행 됩니다. 실제 코드에 길이/표시기 버퍼도 정렬 되어야 합니다.)  
  
 ![SQL 데이터 형식에 기본 C 데이터 형식으로 바인딩](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 에 저장 된 바인딩된 주소 가정는 *주소* 배열에 응용 프로그램에서 다음 식을 사용 하 여 각 열에 바인딩된 메모리에 액세스 합니다.  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 주소에서 두 번째 및 세 번째 열에서 홀수 바이트 시작 바인딩되고 것는 SDWORD의 크기는 4로 나눌 수 없는 주소 세 번째 열에 바인딩되어 있음을 확인 합니다. 일부 컴퓨터에서이 문제가 되지 않습니다는; 다른 사용자에 게에 성능이 약간 저하; 생성 여전히 다른 사람에 치명적인 런타임 오류가 발생 합니다. 더 나은 방법은 해당 자연 맞춤 경계에 바인딩된 각 주소를 맞출 수 있습니다. 값이 1 UCHAR는 검 2이 고는 SDWORD에 대 한 4에 대 한 가정 여기서 "X"가 사용 되는 메모리의 바이트를 나타내며 "O"는 사용 되는 메모리의 바이트 다음 그림에 표시 된 것 처럼 제공할 수 있습니다.  
  
 ![자연 정렬 경계로 바인딩](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 이 솔루션으로 사용 하지 않는 모든 응용 프로그램의 메모리 동안 맞춤 문제가 발생 하지는 않습니다. 에이 솔루션을 구현 하는 코드에 대 한 상당한 양의 각 열의 형식에 따라 개별적으로 정렬 해야 합니다. 가장 큰 맞춤 경계는 4의 크기에 모든 열에 맞게 보다 간단한 솔루션은 다음 그림에 표시 된 예에서입니다.  
  
 ![최대 정렬 경계로 바인딩](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 이 솔루션에 더 큰 구멍 해제 되지만 상대적으로 간단 하 고 빠르게 구현 하의 코드가입니다. 대부분의 경우가 사용 되지 않는 메모리에서 유료 페널티에 만큼 오프셋 합니다. 이 메서드를 사용 하는 예제를 참조 하십시오. [를 사용 하 여 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)합니다.

