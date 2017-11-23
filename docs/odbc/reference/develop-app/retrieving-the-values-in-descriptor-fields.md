---
title: "설명자 필드의 값을 검색할 | Microsoft Docs"
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
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f865e8372ba50cf2e6ee2bcfcf24863284cdd31
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>설명자 필드에 값 검색
응용 프로그램에서 호출할 수 **SQLGetDescField** 설명자 레코드의 단일 필드를 가져올 수 있습니다. **SQLGetDescField** ODBC에 정의 된 모든 설명자 필드에 시작 및 끝 드라이버에서 정의 된 필드에도 응용 프로그램 액세스를 제공 합니다.  
  
 **SQLGetDescRec** 열 또는 매개 변수 데이터의 저장소 및 데이터 형식에 영향을 주는 여러 설명자 필드의 설정을 검색 하기 위해 호출할 수 있습니다.
