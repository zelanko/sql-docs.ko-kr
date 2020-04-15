---
title: 명시적으로 할당된 설명자 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9950bc23a1e75606316039e6c2d66f3dba59940
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305694"
---
# <a name="explicitly-allocated-descriptors"></a>명시적으로 할당된 설명자
응용 프로그램은 데이터베이스에 연결될 때마다 연결에 응용 프로그램 설명기를 명시적으로 할당할 수 있습니다. **SQLSetStmtAttr을**사용 하 여 문 핸들의 특성으로 해당 설명자 핸들을 지정 하 여 응용 프로그램은 해당 암시적으로 할당 된 응용 프로그램 설명자 대신 해당 설명기를 사용 하 여 드라이버를 지시 합니다. 응용 프로그램은 대체 구현 설명자(설명자)를 지정할 수 없습니다.  
  
 응용 프로그램은 명시적으로 할당된 설명자와 두 개 이상의 문을 연결할 수 있습니다. 응용 프로그램이 실제로 데이터베이스에 연결되어 있는 경우에만 설명자가 명시적으로 할당된 설명자가 될 수 있습니다. 응용 프로그램은 이러한 설명자가 명시적으로 해제하거나 연결을 해제하여 암시적으로 해제할 수 있습니다.
