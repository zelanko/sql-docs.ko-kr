---
description: 설명자 복사
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90f3acb5ccb479ba5c1d1eb4c405a486f7032f3f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465872"
---
# <a name="copying-descriptors"></a>설명자 복사
**Sqlcopydesc** 함수를 호출 하 여 한 설명자의 필드를 다른 설명자에 복사 합니다. 필드는 응용 프로그램 설명자 또는 IPD 복사할 수 있지만 IRD에 복사할 수는 없습니다. 모든 유형의 설명자에서 필드를 복사할 수 있습니다. 원본 설명자와 대상 설명자 모두에 대해 정의 된 필드만 복사 됩니다. 설명자의 할당 유형을 변경할 수 없으므로 **Sqlcopydesc** 는 SQL_DESC_ALLOC_TYPE 필드를 복사 하지 않습니다. 복사 된 필드는 기존 필드를 덮어씁니다.  
  
 하나의 문 핸들을 사용 하는 경우 다른 문 핸들의 APD로 사용할 수 있습니다. 이렇게 하면 응용 프로그램 수준에서 데이터를 복사 하지 않고 테이블 간에 행을 복사할 수 있습니다. 이렇게 하기 위해 테이블의 인출 된 행을 설명 하는 행 설명자가 INSERT 문의 매개 변수에 대 한 매개 변수 설명자로 다시 사용 됩니다. 이 작업이 성공 하려면 SQL_MAX_CONCURRENT_ACTIVITIES 정보 유형이 1 보다 커야 합니다.
