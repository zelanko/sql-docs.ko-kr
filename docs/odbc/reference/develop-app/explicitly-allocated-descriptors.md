---
title: 명시적으로 할당 된 설명자 | Microsoft Docs
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
ms.openlocfilehash: 5808265a9ab70b9947cea64fef790497c7229da8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069934"
---
# <a name="explicitly-allocated-descriptors"></a>명시적으로 할당된 설명자
응용 프로그램은 언제 든 지 데이터베이스에 연결 되어 있는 연결에 응용 프로그램 설명자를 명시적으로 할당할 수 있습니다. **SQLSetStmtAttr**를 사용 하 여 문 핸들의 특성으로 해당 설명자 핸들을 지정 하면 응용 프로그램에서 해당 설명자를 사용 하 여 암시적으로 할당 된 해당 응용 프로그램 설명자 대신 해당 설명자를 사용 하도록 지시 합니다. 응용 프로그램에서 대체 구현 설명자를 지정할 수 없습니다.  
  
 응용 프로그램은 명시적으로 할당 된 설명자를 둘 이상의 문과 연결할 수 있습니다. 응용 프로그램이 실제로 데이터베이스에 연결 된 경우에만 설명자가 명시적으로 할당 된 설명자가 될 수 있습니다. 응용 프로그램은 이러한 설명자를 명시적으로 해제 하거나 연결을 해제 하 여 암시적으로 해제할 수 있습니다.
