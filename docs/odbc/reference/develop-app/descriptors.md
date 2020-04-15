---
title: 설명자 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca8299daae744fb9398ed6ffc99c838ce8edff48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305904"
---
# <a name="descriptors"></a>설명자
설명자 핸들은 열 또는 동적 매개 변수에 대한 정보를 포함하는 데이터 구조를 나타냅니다.  
  
 열 및 매개 변수 데이터에서 작동하는 ODBC 함수는 설명자 필드를 암시적으로 설정하고 검색합니다. 예를 **들어, SQLBindCol이** 열 데이터를 바인딩하도록 호출되면 바인딩을 완전히 설명하는 설명자 필드를 설정합니다. **SQLColAttribute열** 데이터를 설명하기 위해 호출되면 설명자 필드에 저장된 데이터를 반환합니다.  
  
 ODBC 함수를 호출하는 응용 프로그램은 설명자 자체에 문제가 되지 않아도 됩니다. 데이터베이스 작업을 수행하면 응용 프로그램이 설명자에 직접 액세스할 필요가 없습니다. 그러나 일부 응용 프로그램의 경우 설명자에 직접 액세스하면 많은 작업이 간소화됩니다. 예를 들어 설명자에 직접 액세스하면 열 데이터를 다시 바인딩할 수 있는 방법을 제공하므로 **SQLBindCol을** 다시 호출하는 것보다 더 효율적일 수 있습니다.  
  
> [!NOTE]  
>  설명자의 물리적 표현은 정의되지 않습니다. 응용 프로그램은 설명자 핸들을 사용하여 ODBC 함수를 호출하여 해당 필드를 조작해야만 설명자에 직접 액세스할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [설명자 형식](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [설명자 필드](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [설명자 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [설명자 필드 가져오기 및 설정](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
