---
title: 일관성 확인 | Microsoft Docs
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
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7be399dc7f8fda9d5223fa6a1749e1849bc9ee88
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="consistency-check"></a>일관성 확인
일관성 확인을 응용 프로그램에서 IPD, 카드가, APD의 SQL_DESC_DATA_PTR 필드가 설정 될 때마다 드라이버에 의해 수행 됩니다. 이 필드를 설정할 때마다 드라이버 SQL_DESC_TYPE 필드의 값과 같은 레코드의 SQL_DESC_TYPE 필드에 적용할 수 있는 값은 유효 하 고 일관성을 확인 합니다.  
  
 일반적으로 IPD의 SQL_DESC_DATA_PTR 필드가 설정 되지 않았습니다. 그러나 응용 프로그램 이렇게 하려면 IPD 필드의 일관성 확인을 적용 합니다. 값으로는 IPD의 SQL_DESC_DATA_PTR 필드가 설정 된 실제로 저장 되지 않으며, 호출 하 여 검색할 수 없습니다 **SQLGetDescField** 또는 **SQLGetDescRec**; 설정을 적용 하기 위해만 이루어집니다는 일관성 확인입니다. IRD에서 일관성 확인을 수행할 수 없습니다.  
  
 일관성 확인에 대 한 자세한 내용은 참조 하십시오. [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.
