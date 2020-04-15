---
title: 설명자 복사 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e2e5897afc3673a21396e256df04d25008c8cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301672"
---
# <a name="copying-descriptors"></a>설명자 복사
**SQLCopyDesc** 함수는 한 설명자의 필드를 다른 설명자로 복사하기 위해 호출됩니다. 필드는 응용 프로그램 설명자 또는 IPD에만 복사할 수 있지만 IRD에는 복사할 수 없습니다. 필드는 모든 유형의 설명자에서 복사할 수 있습니다. 원본 및 대상 설명자 모두에 대해 정의된 필드만 복사됩니다. **SQLCopyDesc는** 설명자의 할당 유형을 변경할 수 없으므로 SQL_DESC_ALLOC_TYPE 필드를 복사하지 않습니다. 복사된 필드는 기존 필드를 덮어씁니다.  
  
 한 문 핸들의 ARD는 다른 명령문 핸들의 APD 역할을 할 수 있습니다. 이렇게 하면 응용 프로그램이 응용 프로그램 수준에서 데이터를 복사하지 않고 테이블 간에 행을 복사할 수 있습니다. 이렇게 하려면 테이블의 가져온 행을 설명하는 행 설명자가 INSERT 문의 매개 변수에 대한 매개 변수 설명자로 다시 사용됩니다. 이 작업이 성공하려면 SQL_MAX_CONCURRENT_ACTIVITIES 정보 형식이 1보다 커야 합니다.
