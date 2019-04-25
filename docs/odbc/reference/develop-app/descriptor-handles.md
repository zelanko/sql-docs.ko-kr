---
title: 설명자 핸들 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3aa085cc0a098f557ca7a8cbddcd787a178b79d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62760764"
---
# <a name="descriptor-handles"></a>설명자 핸들
A *설명자* 응용 프로그램 또는 드라이버에 표시 되는 SQL 문의 매개 변수 또는 결과 집합의 열을 설명 하는 메타 데이터의 컬렉션 (라고도 합니다 *구현*). 따라서 설명자를 네 가지 역할 중 하나를 작성할 수 있습니다.  
  
-   **응용 프로그램 매개 변수 설명자 (APD)입니다.** SQL 문에서 해당 주소, 길이 및 C 데이터 형식 같은 매개 변수에 바인딩된 응용 프로그램 버퍼에 대 한 정보를 포함 합니다.  
  
-   **IPD (구현 매개 변수 설명자)입니다.** SQL 문에서 해당 SQL 데이터 형식, 길이 및 null 허용 여부 같은 매개 변수 정보를 포함합니다.  
  
-   **응용 프로그램 행 설명자 ()입니다.** 해당 주소, 길이 및 C 데이터 형식과 같은 결과 집합의 열에 바인딩된 응용 프로그램 버퍼에 대 한 정보를 포함 합니다.  
  
-   **구현 행 설명자 (IRD)입니다.** 결과 집합을 해당 SQL 데이터 형식, 길이 및 null 허용 여부 등의 열에 대 한 정보를 포함합니다.  
  
 (하나의 입력 역할당) 4 설명자 문을 할당 될 때 자동으로 할당 됩니다. 이러한 라고 *설명자를 자동으로 할당* 되며 항상 해당 문과 사용 하 여 연결 합니다. 응용 프로그램 설명자를 사용 하 여 할당할 수도 **SQLAllocHandle**합니다. 이러한 라고 *설명자를 명시적으로 할당*합니다. 이러한 연결에 할당 되 고 해당 문에서 APD 또는 카드가의 역할을 수행 하려면 해당 연결에서 하나 이상의 문과 사용 하 여 연결할 수 있습니다.  
  
 응용 프로그램에서 명시적 설명자 사용 하지 않고 ODBC에서 대부분의 작업을 수행할 수 있습니다. 그러나 설명자 일부 작업에 대 한 편리한 바로 가기를 제공합니다. 예를 들어, 응용 프로그램에서 서로 다른 두 개의 버퍼에서에서 데이터를 삽입 하려고 합니다. 버퍼의 첫 번째 집합을 사용 하려면가 반복적으로 호출 됩니다. **SQLBindParameter** 매개 변수에 바인딩할는 **삽입** 문을 다음 문을 실행 합니다. 버퍼의 두 번째 집합을 사용 하려면이 프로세스를 반복 하 합니다. 또는 하나의 설명자에서 버퍼의 첫 번째 집합을 다른 설명자에는 버퍼의 두 번째 집합에 바인딩을 설정할 수 없습니다 것입니다. 바인딩 집합 사이 전환 하려면 응용 프로그램 호출 **SQLSetStmtAttr** APD로 문을 사용 하 여 올바른 설명자를 연결 합니다.  
  
 설명자에 대 한 자세한 내용은 참조 하세요. [설명자의 형식이](../../../odbc/reference/develop-app/types-of-descriptors.md)합니다.
