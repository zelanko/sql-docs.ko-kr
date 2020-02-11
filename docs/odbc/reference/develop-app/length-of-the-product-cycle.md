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
ms.openlocfilehash: 203ad92dd6abfc71b0fdeddc466752612e666cee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100449"
---
# <a name="length-of-the-product-cycle"></a>제품 주기의 길이
상호 운용성에 대 한 최종 질문은 시간입니다. 상호 운용 가능한 응용 프로그램을 개발 하는 작업은 일반적으로 상호 운용할 필요가 없는 응용 프로그램을 개발 하는 그 이유는 응용 프로그램에서 DBMS 기능을 확인 하 고, Dbms 마다 동일한 작업을 수행 하 고, 일부 Dbms에서 지 원하는 기능을 해결 하는 등의 작업을 수행 해야 하기 때문입니다.  
  
 개발 시간 외에 제품 수명을 고려해 야 합니다. 한 DBMS에서 다른 DBMS로 마이그레이션할 때 데이터를 전송 하는 응용 프로그램과 같이 응용 프로그램을 한 번 사용 하도록 디자인 된 경우에는 상호 운용할 수 있는 지점이 없습니다. 응용 프로그램은 한 번 사용 되 고 삭제 됩니다.  
  
 응용 프로그램이 오랜 시간 동안 존재 하는 경우 상호 운용 가능한 응용 프로그램으로 유지 관리 하는 것이 더 쉬울 수 있습니다. 단일 DBMS를 대상으로 하는 사용자 지정 응용 프로그램의 경우에도 마찬가지입니다. 그 이유는 상호 운용 가능한 코드가 데이터베이스 기능의 제한 된 하위 집합을 사용 하기 때문입니다. 기본 DBMS를 변경 하는 경우에도 이러한 기능을 사용 가능 하 게 유지 하려면 드라이버가 필요 합니다. 따라서 상호 운용할 수 있는 코드는 응용 프로그램 개발자에서 드라이버 개발자에 이르기까지 DBMS에 대 한 변경 내용으로 인해 복사할 부담을 전환할 수 있습니다.
