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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: edd946ca865cd9d8d2edff2c7bedbb3b2629c97c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299003"
---
# <a name="consistency-check"></a>일관성 검사
응용 프로그램에서 APD, IPD 또는의 SQL_DESC_DATA_PTR 필드를 설정 하면 자동으로 일관성 확인이 수행 됩니다. 이 필드가 설정 될 때마다 드라이버는 SQL_DESC_TYPE 필드의 값과 같은 레코드의 SQL_DESC_TYPE 필드에 적용 가능한 값이 유효 하 고 일관적인 지 확인 합니다.  
  
 IPD의 SQL_DESC_DATA_PTR 필드는 일반적으로 설정 되지 않습니다. 그러나 IPD 필드에 대 한 일관성 확인을 강제 적용 하기 위해 응용 프로그램에서이 작업을 수행할 수 있습니다. IPD의 SQL_DESC_DATA_PTR 필드가로 설정 된 값은 실제로 저장 되지 않으며 **SQLGetDescField** 또는 **SQLGetDescRec**를 호출 하 여 검색할 수 없습니다. 이 설정은 일관성 확인을 강제 적용 하는 경우에만 수행 됩니다. IRD에 대해 일관성 확인을 수행할 수 없습니다.  
  
 일관성 확인에 대 한 자세한 내용은 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)를 참조 하세요.
