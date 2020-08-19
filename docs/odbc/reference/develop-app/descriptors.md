---
description: 설명자
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae01f093ef1b67f1326f8aa7719b74100fcba462
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429335"
---
# <a name="descriptors"></a>설명자
설명자 핸들은 열 또는 동적 매개 변수에 대 한 정보를 포함 하는 데이터 구조를 참조 합니다.  
  
 열 및 매개 변수 데이터에서 작동 하는 ODBC 함수는 암시적으로 설명자 필드를 설정 하 고 검색 합니다. 예를 들어 열 데이터를 바인딩하기 위해 **SQLBindCol** 가 호출 되는 경우 바인딩을 완전히 설명 하는 설명자 필드를 설정 합니다. **Sqlcolattribute** 를 호출 하 여 열 데이터를 설명할 때 설명자 필드에 저장 된 데이터를 반환 합니다.  
  
 ODBC 함수를 호출 하는 응용 프로그램은 설명자와는 관련이 없습니다. 데이터베이스 작업을 수행 하려면 응용 프로그램이 설명자에 대 한 직접 액세스 권한을 얻어야 합니다. 그러나 일부 응용 프로그램의 경우 설명자에 대 한 직접 액세스를 통해 많은 작업을 간소화할 수 있습니다. 예를 들어 설명자에 대 한 직접 액세스는 열 데이터를 다시 바인딩하는 방법을 제공 하며이는 **SQLBindCol** 를 다시 호출 하는 것 보다 효율적일 수 있습니다.  
  
> [!NOTE]  
>  설명자의 물리적 표현이 정의 되어 있지 않습니다. 응용 프로그램은 설명자 핸들을 사용 하 여 ODBC 함수를 호출 하 여 해당 필드를 조작 하는 방법 으로만 설명자에 직접 액세스할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [설명자 형식](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [설명자 필드](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [설명자 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [설명자 필드 가져오기 및 설정](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
