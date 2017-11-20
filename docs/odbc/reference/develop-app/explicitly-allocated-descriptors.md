---
title: "설명자를 명시적으로 할당 | Microsoft Docs"
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
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a4679fa6c6d2185f6e474407882080fea6b7c8a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="explicitly-allocated-descriptors"></a>명시적으로 할당 된 설명자
응용 프로그램에서 언제 든 지 데이터베이스에 연결 되어 연결 된 응용 프로그램 설명자를 할당할 명시적으로 수 있습니다. 사용 하 여 처리 하는 문 특성 처럼이 설명자 핸들을 지정 하 여 **SQLSetStmtAttr**, 응용 프로그램 지시 드라이버에 해당 하는 대신 해당 설명자 암시적으로 응용 프로그램 할당 설명자입니다. 응용 프로그램 대체 구현을 설명자를 지정할 수 없습니다.  
  
 응용 프로그램에서는 명시적으로 할당 된 설명자를 둘 이상의 문을 연결할 수 있습니다. 응용 프로그램은 데이터베이스에 연결 하는 경우에 될 수 있습니다 설명자를 명시적으로 할당 된 설명자입니다. 응용 프로그램 수 있음 설명자를 명시적으로 또는 암시적으로 연결을 해제 하 여 합니다.

