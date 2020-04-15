---
title: 설명자 핸들 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed0595c97f3f4ad92d976c89327a01e25cb5b753
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305914"
---
# <a name="descriptor-handles"></a>설명자 핸들
*설명자는* 응용 프로그램 또는 *드라이버(구현이라고도*함)에서 볼 수 있는 SQL 문의 매개 변수 또는 결과 집합의 열을 설명하는 메타데이터 모음입니다. 따라서 설명자는 다음 네 가지 역할 중 한 가지 를 채울 수 있습니다.  
  
-   **응용 프로그램 매개 변수 설명자(APD).** SQL 문의 매개 변수에 바인딩된 응용 프로그램 버퍼에 대 한 정보(예: 주소, 길이 및 C 데이터 형식)를 포함 합니다.  
  
-   **IPD(구현 매개 변수 설명자).** SQL 데이터 형식, 길이 및 null가능성과 같은 SQL 문의 매개 변수에 대한 정보를 포함합니다.  
  
-   **응용 프로그램 행 설명자(ARD).** 주소, 길이 및 C 데이터 유형과 같은 결과 집합의 열에 바인딩된 응용 프로그램 버퍼에 대한 정보를 포함합니다.  
  
-   **구현 행 설명자(IRD).** SQL 데이터 형식, 길이 및 null가능성과 같은 결과 집합의 열에 대한 정보를 포함합니다.  
  
 문이 할당될 때 4개의 설명자(각 역할을 채우는 설명자 1개)가 자동으로 할당됩니다. 이러한 *설명자는 자동으로 할당된 설명자로* 알려져 있으며 항상 해당 명령문과 연결됩니다. 응용 프로그램은 **SQLAllocHandle**을 사용하여 설명자도 할당할 수 있습니다. 이를 명시적으로 *할당된 설명자라고 합니다.* 연결에 할당되며 해당 연결에 대한 하나 이상의 명령문과 연결하여 해당 명령문에 대한 APD 또는 ARD의 역할을 수행할 수 있습니다.  
  
 ODBC의 대부분의 작업은 응용 프로그램에서 설명자(설명자)를 명시적으로 사용하지 않고 수행할 수 있습니다. 그러나 설명자는 일부 작업에 편리한 바로 가기를 제공합니다. 예를 들어 응용 프로그램이 서로 다른 두 버퍼 집합의 데이터를 삽입하려고 한다고 가정합니다. 첫 번째 버퍼 집합을 사용 하려면 **SQLBindParameter를** 반복적으로 호출 하여 **INSERT** 문의 매개 변수에 바인딩한 다음 문을 실행합니다. 두 번째 버퍼 집합을 사용하려면 이 프로세스를 반복합니다. 또는 한 설명자의 첫 번째 버퍼 집합과 다른 설명자의 두 번째 버퍼 집합에 대한 바인딩을 설정할 수 있습니다. 바인딩 집합 간에 전환하려면 응용 프로그램은 **SQLSetStmtAttr을** 호출하고 올바른 설명자와 APD로 문과 연결합니다.  
  
 설명자에 대한 자세한 내용은 [설명자 유형을](../../../odbc/reference/develop-app/types-of-descriptors.md)참조하십시오.
