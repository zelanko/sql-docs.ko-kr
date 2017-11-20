---
title: Record Count | Microsoft Docs
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
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0d88974bb478386147761a413752e3a69e71a415
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="record-count"></a>Record Count
설명자의 SQL_DESC_COUNT 헤더 필드는 데이터를 포함 하는 번호가 가장 큰 레코드의 1부터 시작 하는 인덱스입니다. 이 필드는 모든 열 또는 바인딩된 매개 변수 수는 없습니다. 설명자가 할당 되 면 SQL_DESC_COUNT의 초기 값은 0입니다.  
  
 드라이버를 할당 하 고 설명자 정보를 저장 하는 데 필요한 모든 저장소를 유지 관리 하는 데 필요한 모든 작업을 수행 합니다. 응용 프로그램은 명시적으로 설명자의 크기를 지정도 새 레코드를 할당 합니다. 누구의 번호 SQL_DESC_COUNT의 값 보다 높습니다. 설명자 레코드에 대 한 정보를 제공 하는 응용 프로그램, 드라이버 SQL_DESC_COUNT를 자동으로 증가 합니다. 가장 높은 설명자 레코드 바인딩 해제 하는 응용 프로그램, 드라이버 SQL_DESC_COUNT 가장 높은 나머지 바인딩된 레코드 번호를 포함 하도록 자동으로 줄어듭니다.

