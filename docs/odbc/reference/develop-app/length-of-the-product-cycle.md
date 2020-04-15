---
title: 제품 주기 길이 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d235146ffe1b4699f0064c5772407bcf40ae962
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306196"
---
# <a name="length-of-the-product-cycle"></a>제품 주기의 길이
상호 운용성에 대한 마지막 질문은 시간입니다. 상호 운용 가능한 응용 프로그램을 개발하는 데는 일반적으로 상호 운용할 수 없는 응용 프로그램을 개발하는 것보다 더 오래 걸립니다. 그 이유는 응용 프로그램이 DBMS 기능을 확인하고, 다른 DBMS에 대해 동일한 작업을 다르게 수행하고, 일부 DBMS에서 지원하지만 다른 DBMS에서는 지원되지 않는 기능 등을 해결해야 하기 때문입니다.  
  
 개발 시간 외에도 제품 수명을 고려해야 합니다. 한 DBMS에서 다른 DBMS로 마이그레이션할 때 데이터를 전송하는 응용 프로그램과 같이 응용 프로그램을 한 번 사용하도록 설계된 경우 상호 운용할 수 있습니다. 응용 프로그램은 한 번 사용되며 폐기됩니다.  
  
 응용 프로그램이 오랫동안 존재하는 경우 상호 운용 가능한 응용 프로그램으로 유지 관리하는 것이 더 쉬울 수 있습니다. 단일 DBMS가 대상으로 있는 사용자 지정 응용 프로그램에도 마찬가지입니다. 그 이유는 상호 운용 가능한 코드는 데이터베이스 기능의 제한된 하위 집합을 사용하기 때문입니다. 기본 DBMS가 변경된 경우에도 드라이버는 이러한 기능을 계속 사용할 수 있도록 유지해야 합니다. 따라서 상호 운용 가능한 코드는 DBMS의 변경 사항에 대처하는 부담을 응용 프로그램 개발자에서 드라이버 개발자로 옮길 수 있습니다.
