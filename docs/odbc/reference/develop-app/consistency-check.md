---
title: 일관성 확인 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 419e338a5e96821606dc26a53a4fccecbc72ae3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125534"
---
# <a name="consistency-check"></a>일관성 검사
일관성 확인을 응용 프로그램에서 IPD, 카드가, APD의 SQL_DESC_DATA_PTR 필드가 설정 될 때마다 드라이버에 의해 수행 됩니다. 이 필드를 설정할 때마다 SQL_DESC_TYPE 필드의 값과 동일한 레코드의 SQL_DESC_TYPE 필드에 적용할 수 있는 값이 유효 하 고 일치는 드라이버를 확인 합니다.  
  
 IPD의 SQL_DESC_DATA_PTR 필드가 일반적으로 설정 되지 않은; 그러나 응용 프로그램 이렇게 IPD 필드의 일관성 확인을 적용 합니다. IPD의 SQL_DESC_DATA_PTR 필드가 설정 된 값은 실제로 저장 되지 않으며를 호출 하 여 검색할 수 없습니다 **SQLGetDescField** 하거나 **SQLGetDescRec**; 강제로에 설정 됩니다는 일관성 확인 합니다. IRD의 일관성 확인을 수행할 수 없습니다.  
  
 일관성 확인에 대 한 자세한 내용은 참조 하세요. [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.
