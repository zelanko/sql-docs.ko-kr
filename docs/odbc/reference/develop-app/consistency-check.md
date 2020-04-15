---
title: 일관성 검사 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: edd946ca865cd9d8d2edff2c7bedbb3b2629c97c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299003"
---
# <a name="consistency-check"></a>일관성 검사
응용 프로그램이 APD, ARD 또는 IPD의 SQL_DESC_DATA_PTR 필드를 설정할 때마다 드라이버가 일관성 검사를 자동으로 수행합니다. 이 필드를 설정할 때마다 드라이버는 SQL_DESC_TYPE 필드의 값과 동일한 레코드의 SQL_DESC_TYPE 필드에 적용되는 값이 유효하고 일관적이있는지 확인합니다.  
  
 IPD의 SQL_DESC_DATA_PTR 필드는 일반적으로 설정되지 않습니다. 그러나 응용 프로그램은 IPD 필드의 일관성 검사를 강제로 수행할 수 있습니다. IPD의 SQL_DESC_DATA_PTR 필드가 실제로 저장되지 않으며 **SQLGetDescField** 또는 **SQLGetDescRec에**대한 호출로 검색할 수 없습니다. 이 설정은 일관성 검사를 강제로 하기 위해서만 만들어집니다. IRD에서 일관성 검사를 수행할 수 없습니다.  
  
 일관성 검사에 대한 자세한 내용은 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)을 참조하십시오.
