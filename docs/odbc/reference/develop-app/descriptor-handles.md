---
title: "설명자 핸들과 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be9387fd0b34123e1a0b903795b1bf1e2106d725
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="descriptor-handles"></a>설명자 핸들
A *설명자* 응용 프로그램 또는 드라이버에서 인식 되는 SQL 문의 매개 변수 또는 결과 집합의 열에 설명 하는 메타 데이터의 컬렉션 (라고도 *구현*). 따라서 설명자를 4 개의 역할 중 하나를 작성할 수 있습니다.  
  
-   **응용 프로그램 매개 변수 설명자 (APD)입니다.** 주소, 길이, C 데이터 형식 등는 SQL 문의 매개 변수에 바인딩된 응용 프로그램 버퍼에 대 한 정보를 포함 합니다.  
  
-   **매개 변수 IPD (구현 설명자)입니다.** SQL 데이터 형식, 길이, null 허용 여부 등는 SQL 문의 매개 변수에 대 한 정보가 포함 됩니다.  
  
-   **응용 프로그램 행 설명자 ()입니다.** 주소, 길이, C 데이터 형식 등의 결과 집합의 열에 바인딩된 응용 프로그램 버퍼에 대 한 정보를 포함 합니다.  
  
-   **구현 행 설명자 IRD ()입니다.** 해당 SQL 데이터 형식, 길이 및 null 허용 여부 등의 결과 집합의 열에 대 한 정보를 포함합니다.  
  
 4 개의 설명자 (하나의 채우는 각 역할)는 문을 할당 될 때 자동으로 할당 됩니다. 이 라고 *자동으로 할당 되어 설명자* 는 항상 해당 문이와 연결 합니다. 응용 프로그램으로 설명자를 할당할 수도 **SQLAllocHandle**합니다. 이 라고 *설명자를 명시적으로 할당*합니다. 이러한 연결에 할당 되 고 하나 이상의 문과 해당 문에서 APD 또는 카드가의 역할을 수행 하려면 해당 연결에서 연결 될 수 있습니다.  
  
 응용 프로그램에서 설명자를 명시적으로 사용 하지 않고 ODBC에서 대부분의 작업을 수행할 수 있습니다. 그러나 설명자 일부 작업에 대 한 편리한 바로 가기를 제공합니다. 예를 들어, 응용 프로그램을 서로 다른 두 개의 버퍼에서에서 데이터를 삽입 하려고 합니다. 버퍼의 첫 번째 집합을 사용 하려면가 반복적으로 호출 됩니다. **SQLBindParameter** 의 매개 변수를 바인딩하는 **삽입** 문을 다음 문을 실행 합니다. 버퍼의 두 번째 집합을 사용 하려면 것이 프로세스를 반복 합니다. 또는 바인딩을 하나의 설명자 버퍼의 첫 번째 집합을 두 번째 집합이 다른 설명자의 버퍼를 설정할 수 없습니다 것입니다. 바인딩 집합 사이 전환 하려면 응용 프로그램 동작만 호출 **SQLSetStmtAttr** APD로 문을 사용 하 여 올바른 설명자를 연결 하 고 있습니다.  
  
 설명자에 대 한 자세한 내용은 참조 [설명자 형식](../../../odbc/reference/develop-app/types-of-descriptors.md)합니다.
