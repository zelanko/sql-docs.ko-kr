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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3d75a78a5eaa516921e561cb2d34786804d182
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="obtaining-descriptor-handles"></a>처리 설명자 얻기
응용 프로그램이에 대 한 호출의 출력 인수로 모든 명시적으로 할당 된 설명자 핸들을 가져오면 **SQLAllocHandle**합니다. 호출 하 여 암시적으로 할당 된 설명자 핸들 가져옵니다 **SQLGetStmtAttr**합니다.

