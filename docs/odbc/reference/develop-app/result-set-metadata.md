---
title: 결과 세트 메타데이터 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b78cdeb4c8b3522f4677c0277401cd9395a36a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300083"
---
# <a name="result-set-metadata"></a>결과 집합 메타데이터
*메타데이터는* 다른 데이터를 설명하는 데이터입니다. 예를 들어 결과 집합 메타데이터는 결과 집합의 열 수, 해당 열의 데이터 유형, 이름, 정밀도, nullability 등과 같은 결과 집합을 설명합니다.  
  
 상호 운용 가능한 응용 프로그램은 항상 결과 집합 열의 메타데이터를 확인해야 합니다. 결과 집합의 열메타데이터는 카탈로그 함수에서 반환되는 열의 메타데이터와 다를 수 있습니다. 예를 들어 두 테이블을 조인하여 만든 결과 집합에 업데이터 열이 포함되어 있다고 가정합니다. **SQLColumnPrivileges는** 사용자가 열을 업데이트할 수 있음을 나타낼 수 있지만, 열이 조인의 "다수" 쪽에 있는 경우 결과 집합 메타데이터가 아닐 수 있습니다. 많은 데이터 원본은 조인의 "일쪽" 쪽에 있는 열을 업데이트할 수 있지만 "다"쪽에는 업데이트할 수 없습니다. 데이터 원본이 결과 집합을 만드는 동안 데이터 형식을 승격시킬 수 있으므로 데이터 형식도 동일하다고 가정할 수 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [메타데이터는 어떻게 사용되나요?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
