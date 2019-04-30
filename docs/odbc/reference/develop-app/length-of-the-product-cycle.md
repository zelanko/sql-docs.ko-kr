---
title: 제품 주기의 길이 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c8a5b88f3fdca03be7740ba086e7ff61edbf684
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127225"
---
# <a name="length-of-the-product-cycle"></a>제품 주기의 길이
상호 운용성에 대 한 마지막 질문 시간입니다. 일반적으로 상호 운용 가능한 응용 프로그램을 개발 noninteroperable 단일 개발 보다 더 오래 걸립니다. 이유는 응용 프로그램 DBMS 기능을 확인, 다양 한 Dbms에 대 한 동일한 작업을 다르게 수행, 다른 것 이지만 일부 Dbms에서 지 원하는 기능을 해결 하며 등입니다.  
  
 개발 시간 외에도 제품 수명을 고려해 야 합니다. 데 한 번 다른 하나의 DBMS에서 마이그레이션할 경우 데이터를 전송 하는 응용 프로그램과 같은 응용 프로그램 설계 된 경우 상호 운용 가능한 만드는 지점이 있습니다. 응용 프로그램이 한 번 사용 되며 삭제 합니다.  
  
 응용 프로그램은 오랜 시간 동안 존재 하는 경우에 쉽게 상호 운용 가능한 응용 프로그램으로 유지 관리할 수 있습니다. 대상으로 단일 DBMS에 있는 사용자 지정 응용 프로그램에 대해서도 마찬가지입니다. 이유는 상호 운용 가능한 코드는 데이터베이스 기능에 제한 된 하위 집합입니다. 드라이버는 기본 dbms 변경 되어도 사용할 수 있는 이러한 기능을 유지 해야 합니다. 따라서 상호 운용 가능한 코드 드라이버 개발자에 게 응용 프로그램 개발자의 dbms 대처 변경 하는 것의 부담을 바꿀 수 있습니다.
