---
title: 레코드 수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28e503ae4602d87fc9138ed018ee1e95f135ec57
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281819"
---
# <a name="record-count"></a>Record Count
설명자의 SQL_DESC_COUNT 헤더 필드는 데이터를 포함하는 가장 높은 번호의 레코드의 한 기반 인덱스입니다. 이 필드는 바인딩된 모든 열 또는 매개 변수의 수가 아닙니다. 설명자가 할당되면 SQL_DESC_COUNT 초기 값은 0입니다.  
  
 드라이버는 설명자 정보를 보유하는 데 필요한 저장소를 할당하고 유지하는 데 필요한 모든 작업을 수행합니다. 응용 프로그램은 설명자의 크기를 명시적으로 지정하거나 새 레코드를 할당하지 않습니다. 응용 프로그램이 SQL_DESC_COUNT 값보다 높은 설명자 레코드에 대한 정보를 제공하면 드라이버가 자동으로 SQL_DESC_COUNT 증가합니다. 응용 프로그램이 가장 높은 번호의 설명자 레코드를 바인딩 해제하면 드라이버가 자동으로 SQL_DESC_COUNT 감소하여 가장 높은 남은 바인딩 레코드 수를 포함합니다.
