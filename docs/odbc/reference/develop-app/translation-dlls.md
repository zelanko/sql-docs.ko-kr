---
title: 변환 Dll | Microsoft Docs
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
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ab283e0086afadd5fc5bbd9e465241ca997890e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915967"
---
# <a name="translation-dlls"></a>변환 Dll
응용 프로그램 및 데이터 원본 종종 서로 다른 문자 집합에 데이터를 저장 합니다. ODBC 드라이버에서 하나의 문자를 다른 집합의 데이터를 변환 하는 일반 메커니즘을 제공 합니다. 변환 함수를 구현 하는 DLL 이루어져 **SQLDriverToDataSource** 및 **SQLDataSourceToDriver**, 데이터 원본 사이의 모든 데이터를 변환 하는 드라이버에 의해 호출 됩니다 및 드라이버입니다. 이 DLL 드라이버 개발자 응용 프로그램 개발자가 쓸 수 또는 제 3 자입니다.  
  
 해당 데이터 원본에 대 한 시스템 정보에는 특정 데이터 원본에 대 한 변환 DLL을 지정할 수 있습니다. 자세한 내용은 참조 [데이터 원본에 대 한 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)합니다. 런타임에 SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION 연결 특성을 설정할 수도 있습니다.  
  
 번역 옵션에는 특정 변환 DLL에 의해서만 해석 될 수 있는 값입니다. 예를 들어 변환 DLL 서로 다른 코드 페이지 간의 변환을 담당 합니다 옵션 응용 프로그램 데이터 원본에 의해 사용 되는 코드 페이지 번호를 지정할 수 있습니다. 번역 옵션을 사용 하는 변환 DLL에 대 한 요구 사항이 있습니다.  
  
 DLL가 지정 하는 변환 후 드라이버 로드 및 호출 응용 프로그램 및 데이터 원본 사이의 모든 데이터를 변환 합니다. 데이터 원본에서 검색 하는 모든 문자 결과, 열 이름 및 오류 메시지 등의 문자 메타 데이터 및 모든 SQL 문 및 문자 매개 변수를 데이터 원본에 전송 되 고이 있습니다. 응용 프로그램에 데이터 원본에 연결 될 때까지 변환 DLL 로드 되지 않으므로 연결 데이터가 변환 되지 않습니다.
