---
title: "처리 설명자 얻기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d94b21ff4583682e7013321b3e871aee04ce6da1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="obtaining-descriptor-handles"></a>처리 설명자 얻기
응용 프로그램이에 대 한 호출의 출력 인수로 모든 명시적으로 할당 된 설명자 핸들을 가져오면 **SQLAllocHandle**합니다. 호출 하 여 암시적으로 할당 된 설명자 핸들 가져옵니다 **SQLGetStmtAttr**합니다.
