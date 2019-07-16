---
title: 설명자 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2138a5f8417fc9156c916719e96d707b9a29de9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040014"
---
# <a name="descriptors"></a>설명자
설명자 핸들을 동적 매개 변수 또는 열에 대 한 정보를 포함 하는 데이터 구조를 가리킵니다.  
  
 열 및 매개 변수 데이터에서 암시적으로 실행 되는 ODBC 함수를 설정 및 설명자 필드를 검색 합니다. 예를 들어, **SQLBindCol** 라고 열 데이터를 바인딩할 바인딩을 완벽 하 게 설명 하는 설명자 필드를 설정 합니다. 때 **SQLColAttribute** 라고 열 데이터를 설명 하기 위해 설명자 필드에 저장 된 데이터를 반환 합니다.  
  
 ODBC 함수를 호출 하는 응용 프로그램 설명자를 사용 하 여 자체를 고려할 필요 합니다. 데이터베이스 작업도 응용 프로그램 설명자 직접 액세스할 수 있는지에 필요 합니다. 그러나 일부 응용 프로그램에 대 한 많은 작업 간소화 설명자에 직접 액세스 하지 못하도록 합니다. 예를 들어, 설명자에 대 한 액세스를 통해 호출 보다 더 효율적일 수 있습니다 하는 열 데이터를 다시 바인딩 수를 직접 **SQLBindCol** 다시 합니다.  
  
> [!NOTE]  
>  설명자의 물리적으로 나타낸 정의 되지 않았습니다. 설명자 핸들을 사용 하 여 ODBC 함수를 호출 하 여 해당 필드를 조작에 의해서만 설명자에 대 한 직접 액세스를 확보 하는 응용 프로그램입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [설명자 유형](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [설명자 필드](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [설명자 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [설명자 필드 가져오기 및 설정](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
