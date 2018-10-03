---
title: 설명자를 명시적으로 할당 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbec69e0d984d843abc2b8754e111a1199c79a5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644541"
---
# <a name="explicitly-allocated-descriptors"></a>명시적으로 할당된 설명자
응용 프로그램에는 언제 든 지 데이터베이스에 연결 된 연결에서 응용 프로그램 설명자를 할당할 명시적으로 수 있습니다. 문 특성 처리를 사용 하 여 해당 설명자 핸들을 지정 하 여 **SQLSetStmtAttr**, 응용 프로그램 전달 드라이버에 해당 하는 대신 해당 설명자를 사용 하 여 암시적으로 응용 프로그램 할당 설명자입니다. 응용 프로그램 대체 구현 설명자를 지정할 수 없습니다.  
  
 응용 프로그램에는 둘 이상의 문을 사용 하 여 명시적으로 할당 된 설명자를 연결할 수 있습니다. 응용 프로그램 데이터베이스에 실제로 연결 되어 있는 경우에 설명자 수를 명시적으로 할당 된 설명자입니다. 응용 프로그램 사용 가능한 수 설명자를 명시적으로 또는 암시적으로 해당 연결을 해제 하 여.
