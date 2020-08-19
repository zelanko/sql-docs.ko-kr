---
description: 변환 DLL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88e0fc6879db7e4b370acc62b2d0102b3ef0a375
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421457"
---
# <a name="translation-dlls"></a>변환 DLL
응용 프로그램 및 데이터 원본은 데이터를 다른 문자 집합에 저장 하는 경우가 많습니다. ODBC는 드라이버에서 문자 집합 간에 데이터를 변환 하는 데 사용할 수 있는 일반 메커니즘을 제공 합니다. **SQLDriverToDataSource** 및 **SQLDataSourceToDriver**변환 함수를 구현 하는 DLL로 구성 되며,이는 드라이버에서 데이터 원본 및 드라이버 사이의 모든 데이터를 변환 하기 위해 호출 하는 함수입니다. 이 DLL은 응용 프로그램 개발자, 드라이버 개발자 또는 제 3 자에 의해 작성 될 수 있습니다.  
  
 특정 데이터 원본에 대 한 변환 DLL은 해당 데이터 원본에 대 한 시스템 정보에 지정할 수 있습니다. 자세한 내용은 [데이터 원본 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)를 참조 하세요. SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION 연결 특성을 사용 하 여 런타임에 설정할 수도 있습니다.  
  
 Translation 옵션은 특정 변환 DLL에 의해서만 해석 될 수 있는 값입니다. 예를 들어 변환 DLL이 서로 다른 코드 페이지를 변환 하는 경우이 옵션은 응용 프로그램 및 데이터 소스에서 사용 하는 코드 페이지 수를 제공할 수 있습니다. 변환 DLL에서 translation 옵션을 사용 하기 위한 요구 사항은 없습니다.  
  
 변환 DLL이 지정 된 후 드라이버에서 해당 DLL을 로드 하 고 호출 하 여 응용 프로그램과 데이터 원본 간에 흐르는 모든 데이터를 변환 합니다. 여기에는 데이터 원본으로 전송 되는 모든 SQL 문 및 문자 매개 변수와 모든 문자 결과, 열 이름과 같은 문자 메타 데이터 및 데이터 원본에서 검색 된 오류 메시지가 포함 됩니다. 응용 프로그램이 데이터 원본에 연결 된 후에도 변환 DLL이 로드 되지 않으므로 연결 데이터는 변환 되지 않습니다.
