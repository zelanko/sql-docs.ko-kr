---
title: 결과 집합 메타 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d309136c3682a781d4eef82e69e2a2f98a20efe2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="result-set-metadata"></a>결과 집합 메타 데이터
*메타 데이터* 는 다른 데이터를 설명 하는 데이터입니다. 예를 들어 결과 집합 메타 데이터는 결과 집합은 결과 집합의 열 수, 열, 이름, 전체 자릿수, null 허용 여부, 및 등의 데이터 형식 등을 설명합니다.  
  
 상호 운용 가능한 응용 프로그램의 결과 집합 열 메타 데이터를 항상 확인 해야 합니다. 카탈로그 함수에서 반환 된 결과 집합의 열에 대 한 메타 데이터 열에 대 한 메타 데이터에서 달라질 수 있습니다. 예를 들어, 업데이트할 수 있는 열 두 테이블을 조인 하 여 만든 결과 집합에 포함 됩니다. 반면 **SQLColumnPrivileges** 사용자 열을 업데이트할 수 있습니다, 결과 집합 메타 데이터 열이 조인의 "다" 쪽에 하지는 나타낼 수 있습니다; 여러 데이터 원본에는 없지만 조인의 "일" 쪽에는 열을 업데이트할 수는 " 다"쪽입니다. 데이터 형식까지 데이터 원본의 데이터 형식 결과 집합을 만드는 동안 상태 때문에 동일한 경우를 가정할 수 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [메타 데이터는 어떻게 사용됩니까?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
