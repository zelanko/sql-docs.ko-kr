---
title: 변환 Dll | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1d0e23019f3e5b68ad38711c1f041b160ceb31
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305745"
---
# <a name="translation-dlls"></a>변환 DLL
응용 프로그램 및 데이터 원본 종종 서로 다른 문자 집합에 데이터를 저장 합니다. ODBC 드라이버에서 하나의 문자를 다른 집합의 데이터를 변환 하는 일반 메커니즘을 제공 합니다. 변환 함수를 구현 하는 DLL로 구성 됩니다 **SQLDriverToDataSource** 하 고 **SQLDataSourceToDriver**, 데이터 원본 간에 흐르는 모든 데이터를 변환 하는 드라이버에 의해 호출 됩니다 및 드라이버입니다. 이 DLL에는 드라이버 개발자는 응용 프로그램 개발자가 작성할 수 있습니다 또는 제 3 자입니다.  
  
 해당 데이터 원본에 대 한 시스템 정보에는 특정 데이터 원본에 대 한 번역 DLL을 지정할 수 있습니다. 자세한 내용은 [데이터 소스 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)합니다. 런타임에 SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION 연결 특성을 사용 하 여 설정할 수도 있습니다.  
  
 변환 옵션에는 특정 변환 DLL에 의해서만 해석 될 수 있는 값입니다. 예를 들어 번역을 서로 다른 코드 페이지 간의 변환 DLL 옵션에 응용 프로그램 및 데이터 원본에서 사용 하는 코드 페이지 번호를 지정할 수 있습니다. 변환 옵션을 사용 하는 번역 DLL에 대 한 요구 사항이 있습니다.  
  
 DLL이 지정 된 번역을 드라이버가 로드 후 호출 응용 프로그램 및 데이터 원본 간에 흐르는 모든 데이터를 변환 합니다. 여기에 모든 SQL 문 및 데이터 원본에 전송 되는 문자 매개 변수 및 데이터 원본에서 검색 하는 모든 문자 결과, 열 이름 및 오류 메시지와 같은 문자 메타 데이터입니다. 응용 프로그램 데이터 원본에 연결 된 후까지 변환 DLL 로드 되지 않으므로 연결 데이터 변환 되지 않습니다.
