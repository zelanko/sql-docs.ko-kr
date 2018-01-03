---
title: "처리 설명자 얻기 | Microsoft Docs"
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
helpviewer_keywords: descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 921d3e9bc76ff49b35b58d3b519a4adcc227d241
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="obtaining-descriptor-handles"></a>처리 설명자 얻기
응용 프로그램이에 대 한 호출의 출력 인수로 모든 명시적으로 할당 된 설명자 핸들을 가져오면 **SQLAllocHandle**합니다. 호출 하 여 암시적으로 할당 된 설명자 핸들 가져옵니다 **SQLGetStmtAttr**합니다.
