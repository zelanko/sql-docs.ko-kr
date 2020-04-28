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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b78cdeb4c8b3522f4677c0277401cd9395a36a5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300083"
---
# <a name="result-set-metadata"></a>결과 집합 메타데이터
*메타* 데이터는 다른 데이터를 설명 하는 데이터입니다. 예를 들어 결과 집합 메타 데이터는 결과 집합의 열 수, 해당 열의 데이터 형식, 이름, 전체 자릿수, null 허용 여부 등의 결과 집합을 설명 합니다.  
  
 상호 운용 가능한 응용 프로그램은 항상 결과 집합 열의 메타 데이터를 확인 해야 합니다. 결과 집합의 열에 대 한 메타 데이터는 카탈로그 함수에서 반환 된 열에 대 한 메타 데이터와 다를 수 있습니다. 예를 들어 두 테이블을 조인 하 여 생성 된 결과 집합에 업데이트할 수 있는 열이 포함 되어 있다고 가정 합니다. **Sqlcolumnprivileges** 사용자가 열을 업데이트할 수 있음을 나타낼 수 있지만 열이 조인의 "다" 쪽에 있는 경우 결과 집합 메타 데이터는 그렇지 않을 수 있습니다. 많은 데이터 원본은 조인의 "일" 쪽에서 열을 업데이트할 수 있지만 "다" 쪽에서는 업데이트할 수 없습니다. 데이터 원본에서 결과 집합을 만드는 동안 데이터 형식을 승격할 수 있기 때문에 데이터 형식을 동일한 것으로 간주할 수 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [메타데이터는 어떻게 사용되나요?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
