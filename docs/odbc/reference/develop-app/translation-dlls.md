---
title: 번역 DLL | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3dad12bcd71434c1013b4fde5b4bd0231e56016f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297948"
---
# <a name="translation-dlls"></a>변환 DLL
응용 프로그램 및 데이터 원본은 종종 다른 문자 집합에 데이터를 저장합니다. ODBC는 드라이버가 한 문자 집합에서 다른 문자 집합으로 데이터를 변환할 수 있는 일반적인 메커니즘을 제공합니다. 데이터 원본과 드라이버 간에 흐르는 모든 데이터를 변환하기 위해 드라이버에서 호출되는 변환 함수 **SQLDriverToDataSource** 및 **SQLDataSourceToDriver를**구현하는 DLL로 구성됩니다. 이 DLL은 응용 프로그램 개발자, 드라이버 개발자 또는 타사에서 작성할 수 있습니다.  
  
 특정 데이터 원본에 대한 번역 DLL은 해당 데이터 원본에 대한 시스템 정보에 지정할 수 있습니다. 자세한 내용은 [데이터 원본 사양 하위 키를 참조하십시오.](../../../odbc/reference/install/data-source-specification-subkeys.md) 또한 SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION 연결 특성을 통해 런타임에 설정할 수도 있습니다.  
  
 변환 옵션은 특정 번역 DLL에서만 해석할 수 있는 값입니다. 예를 들어 번역 DLL이 서로 다른 코드 페이지 간에 변환되는 경우 이 옵션은 응용 프로그램과 데이터 원본에서 사용하는 코드 페이지의 번호를 제공할 수 있습니다. 번역 DLL이 번역 옵션을 사용할 필요는 없습니다.  
  
 변환 DLL을 지정한 후 드라이버가 로드하고 호출하여 응용 프로그램과 데이터 원본 간에 흐르는 모든 데이터를 변환합니다. 여기에는 데이터 원본으로 전송되는 모든 SQL 문 및 문자 매개 변수와 모든 문자 결과, 열 이름과 같은 문자 메타데이터 및 데이터 원본에서 검색된 오류 메시지가 포함됩니다. 응용 프로그램이 데이터 원본에 연결될 때까지 변환 DLL이 로드되지 않으므로 연결 데이터가 변환되지 않습니다.
