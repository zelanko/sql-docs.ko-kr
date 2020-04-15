---
title: 설명자 필드 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04f9520e2ef462df481bb104e389aeb57b5dd457
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304154"
---
# <a name="setting-descriptor-fields"></a>설명자 필드 설정
설명자의 필드를 수정하려면 응용 프로그램에서 **SQLSetDescField**를 호출할 수 있습니다. 일부 필드는 읽기 전용이며 설정할 수 없습니다. [(SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명을 참조하십시오.)  
  
 설명자 레코드 필드는 레코드*번호(RecNumber)가*1 이상으로 설정되고 설명자 헤더 필드는 레코드 번호 0으로 설정됩니다. 책갈피가 열 0에 포함되어 있는 규칙에 따라 책갈피 필드를 설정하는 데도 레코드 번호 0이 사용됩니다. 이렇게 하면 책갈피 필드가 설명자 헤더 내에 포함되어 있다는 인상을 남길 수 있지만 그렇지 않습니다. 책갈피 필드는 헤더 필드와 구별됩니다.  
  
 필드를 개별적으로 설정할 때 응용 프로그램은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)에 정의된 순서를 따라야 합니다. 일부 필드를 설정하면 드라이버가 다른 필드를 설정합니다. 이렇게 하면 응용 프로그램에서 데이터 형식을 지정하면 설명자가 항상 사용할 수 있습니다. 응용 프로그램이 SQL_DESC_TYPE 필드를 설정하면 드라이버는 형식을 지정하는 다른 필드가 유효하고 일관적이있는지 확인합니다.  
  
 설명자 필드를 설정하는 함수 호출이 실패하면 실패한 함수 호출 후에 설명자 필드의 내용이 정의되지 않습니다.
