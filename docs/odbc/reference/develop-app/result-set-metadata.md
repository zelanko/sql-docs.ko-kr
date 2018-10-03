---
title: 결과 집합 메타 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dc88892fab2fd18dbcbec5ce54fa09c9c9b89e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819931"
---
# <a name="result-set-metadata"></a>결과 집합 메타데이터
*메타 데이터* 데이터가 다른 데이터에 설명 합니다. 예를 들어 결과 집합 메타 데이터는 결과 집합의 열 수, 열, 이름, 전체 자릿수, null 허용 여부 및 등의 데이터 형식 같은 결과 집합을 설명합니다.  
  
 상호 운용 가능한 응용 프로그램의 결과 집합 열 메타 데이터를 항상 확인 해야 합니다. 카탈로그 함수에서 반환 된 결과 집합의 열에 대 한 메타 데이터 열에 대 한 메타 데이터에서 달라질 수 있습니다. 예를 들어 열을 업데이트할 수 있는 두 테이블을 조인 하 여 만든 결과 집합에 포함 되어 있는지 가정 합니다. 하는 동안 **SQLColumnPrivileges** 사용자 열을 업데이트할 수 있습니다에 결과 집합 메타 데이터 열 조인 "다" 쪽에 있으면 없습니다 수를 나타낼 수 있습니다; 그리고 여러 데이터 원본 "일" 쪽에는 없지만 조인 열을 업데이트할 수는 " 다"쪽입니다. 데이터 원본 데이터 형식 결과 집합을 만드는 동안 상태 때문에 데이터 형식에도 동일 하 가정할 수 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [메타 데이터는 어떻게 사용됩니까?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
