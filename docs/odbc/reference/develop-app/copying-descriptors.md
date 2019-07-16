---
title: 설명자 복사 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d41cd744d39113c556c4ee8bc17411b7992e596
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002145"
---
# <a name="copying-descriptors"></a>설명자 복사
합니다 **SQLCopyDesc** 함수가 호출 되어 다른 설명자에 하나의 설명자 필드를 복사 합니다. IRD 아니라 응용 프로그램 설명자를 또는 IPD 필드를 복사할 수 있습니다. 설명자의 모든 형식에서 필드를 복사할 수 있습니다. 원본 및 대상 모두 설명자에 대해 정의 된 필드에만 복사 됩니다. **SQLCopyDesc** 설명자의 할당 유형을 변경할 수 없으므로 SQL_DESC_ALLOC_TYPE 필드를 복사 하지 않습니다. 복사 된 필드는 기존 필드를 덮어씁니다.  
  
 카드가 하나 문 핸들에서 다른 문 핸들에서 APD 역할도 할 수 있습니다. 이 응용 프로그램을 간에 응용 프로그램 수준에서 데이터를 복사 하지 않고 테이블 행을 복사할 수 있습니다. 이 위해 테이블의 인출한 행에 설명 하는 행 설명자를 문에서 매개 변수에 대해 매개 변수 설명자 다시 사용 됩니다. SQL_MAX_CONCURRENT_ACTIVITIES 정보 유형을이 작업을 수행 하려면 1 보다 커야 합니다.
