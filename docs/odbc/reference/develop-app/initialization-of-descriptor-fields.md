---
title: 설명자 필드의 초기화 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ed6479a60f1d0695107c216b2f0c94a55f68ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300123"
---
# <a name="initialization-of-descriptor-fields"></a>설명자 필드 초기화
응용 프로그램 행 설명자가 할당되면 해당 필드는 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)에 표시된 대로 초기 값을 받습니다. SQL_DESC_TYPE 필드의 초기 값은 SQL_DEFAULT. 이렇게 하면 응용 프로그램에 프레젠테이션을 위한 데이터베이스 데이터의 표준 처리가 제공됩니다. 응용 프로그램은 설명자 레코드의 필드를 설정하여 데이터의 상이한 처리를 지정할 수 있습니다.  
  
 설명자 헤더의 SQL_DESC_ARRAY_SIZE 초기 값은 1입니다. 응용 프로그램은 이 필드를 수정하여 멀티로잉 가져오기를 활성화할 수 있습니다.  
  
 기본값의 개념은 IRD 필드에 대해 유효하지 않습니다. 응용 프로그램은 IRD와 관련된 준비되거나 실행된 문이 있는 경우에만 IRD 필드에 액세스할 수 있습니다.  
  
 IPD의 특정 필드는 IPD가 드라이버에 의해 자동으로 채워진 후에만 정의됩니다. 그렇지 않은 경우 정의되지 않습니다. 이러한 필드는 SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED 및 SQL_DESC_LOCAL_TYPE_NAME.
