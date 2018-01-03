---
title: "설명자 복사 | Microsoft Docs"
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
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6ba44b9cdb214007cb11cadcb1a9f25d80a5f63
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="copying-descriptors"></a>설명자 복사
**SQLCopyDesc** 다른 설명자에 하나의 설명자 필드를 복사 하려면 함수를 호출 합니다. 필드는 IPD 또는 응용 프로그램 설명자에만 속하지만 IRD에 복사할 수 있습니다. 설명자의 모든 형식에서 필드를 복사할 수 있습니다. 소스와 대상 설명자에 대해 정의 된 필드에만 복사 됩니다. **SQLCopyDesc** 설명자의 할당 유형을 변경할 수 없으므로 SQL_DESC_ALLOC_TYPE 필드를 복사 하지 않습니다. 복사한 필드 기존 필드를 덮어씁니다.  
  
 APD 다른 문 핸들에서 하나의 문 핸들에서 카드가 될 수 있습니다. 따라서 응용을 프로그램을 응용 프로그램 수준에서 데이터를 복사 하지 않고 테이블 간에 행을 복사할 수 있습니다. 이 위해 테이블의 인출 된 행에 설명 하는 행 설명자는 INSERT 문에서 매개 변수에 대 한 매개 변수 설명자를 다시 사용 됩니다. SQL_MAX_CONCURRENT_ACTIVITIES 정보 유형을이 작업이 성공 하려면에 대해 1 보다 커야 합니다.
