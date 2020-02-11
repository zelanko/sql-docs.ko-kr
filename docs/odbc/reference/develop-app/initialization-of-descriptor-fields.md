---
title: 설명자 필드 초기화 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c78162bcf0421fee609abe5fcacf9613e0f8020b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138937"
---
# <a name="initialization-of-descriptor-fields"></a>설명자 필드 초기화
응용 프로그램 행 설명자를 할당 하면 해당 필드는 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)에 표시 된 대로 초기 값을 받습니다. SQL_DESC_TYPE 필드의 초기 값은 SQL_DEFAULT입니다. 이를 통해 응용 프로그램에 표시 되는 데이터베이스 데이터의 표준 처리를 사용할 수 있습니다. 응용 프로그램은 설명자 레코드의 필드를 설정 하 여 다른 데이터 처리를 지정할 수 있습니다.  
  
 설명자 헤더에서 SQL_DESC_ARRAY_SIZE의 초기 값은 1입니다. 응용 프로그램은 다중 행 페치를 사용 하도록이 필드를 수정할 수 있습니다.  
  
 기본값의 개념은 IRD의 필드에 사용할 수 없습니다. 응용 프로그램은 준비 된 문이나 실행 된 문이 있는 경우에만 IRD의 필드에 대 한 액세스 권한을 얻을 수 있습니다.  
  
 IPD의 특정 필드는 IPD가 자동으로 드라이버가 채워진 후에만 정의 됩니다. 그렇지 않으면 정의 되지 않습니다. 이러한 필드는 SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED 및 SQL_DESC_LOCAL_TYPE_NAME입니다.
