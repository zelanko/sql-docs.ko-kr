---
description: 설명자 핸들
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 859071eacbfa65f360965cf5c5df17d4fbf6361d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476725"
---
# <a name="descriptor-handles"></a>설명자 핸들
*설명자* 는 응용 프로그램 또는 드라이버 ( *구현이*라고도 함)에서 볼 수 있는 것 처럼 SQL 문 또는 결과 집합의 열에 대 한 매개 변수를 설명 하는 메타 데이터의 컬렉션입니다. 따라서 설명자는 다음 네 가지 역할 중 하나를 채울 수 있습니다.  
  
-   **APD (응용 프로그램 매개 변수 설명자).** SQL 문의 매개 변수에 바인딩된 응용 프로그램 버퍼에 대 한 정보 (예: 주소, 길이 및 C 데이터 형식)를 포함 합니다.  
  
-   **IPD (구현 매개 변수 설명자).** Sql 데이터 형식, 길이 및 null 허용 여부와 같은 SQL 문의 매개 변수에 대 한 정보를 포함 합니다.  
  
-   **응용 프로그램 행 설명자 (기타).** 결과 집합의 열에 바인딩된 응용 프로그램 버퍼에 대 한 정보 (예: 주소, 길이 및 C 데이터 형식)를 포함 합니다.  
  
-   **구현 행 설명자 (IRD).** 결과 집합의 열에 대 한 정보 (예: SQL 데이터 형식, 길이 및 null 허용 여부)를 포함 합니다.  
  
 문이 할당 될 때 4 개의 설명자 (각 역할 채우기 하나)가 자동으로 할당 됩니다. 이러한 *설명자는 자동으로 할당 된 설명자* 라고 하며 항상 해당 문과 연결 됩니다. 응용 프로그램은 **SQLAllocHandle**를 사용 하 여 설명자를 할당할 수도 있습니다. 이를 명시적으로 *할당 된 설명자*라고 합니다. 이러한 규칙은 연결에 할당 되며 해당 문에 대해 APD 또는 사용의 역할을 수행 하기 위해 해당 연결에서 하나 이상의 문과 연결 될 수 있습니다.  
  
 ODBC에서 대부분의 작업은 응용 프로그램에서 설명자를 명시적으로 사용 하지 않고도 수행할 수 있습니다. 그러나 설명자는 일부 작업에 대 한 편리한 바로 가기를 제공 합니다. 예를 들어 응용 프로그램에서 두 개의 서로 다른 버퍼 집합의 데이터를 삽입 하려고 한다고 가정 합니다. 첫 번째 버퍼 집합을 사용 하려면 **SQLBindParameter** 를 반복적으로 호출 하 여 **INSERT** 문의 매개 변수에 바인딩한 다음 문을 실행 합니다. 두 번째 버퍼 집합을 사용 하려면이 프로세스를 반복 합니다. 또는 한 설명자의 첫 번째 버퍼 집합과 다른 설명자의 두 번째 버퍼 집합에 대 한 바인딩을 설정할 수 있습니다. 바인딩 집합 간을 전환 하기 위해 응용 프로그램은 단순히 **SQLSetStmtAttr** 를 호출 하 고 올바른 설명자를 문과 함께 apd에 연결 합니다.  
  
 설명자에 대 한 자세한 내용은 [설명자 형식](../../../odbc/reference/develop-app/types-of-descriptors.md)을 참조 하세요.
