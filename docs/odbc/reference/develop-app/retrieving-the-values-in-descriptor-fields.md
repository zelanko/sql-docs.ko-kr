---
title: 설명자 필드의 값 검색 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43467d19f3f2e576efa0402c4ba513e23da59390
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304324"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>설명자 필드에서 값 검색
응용 프로그램은 **SQLGetDescField를** 호출하여 설명자 레코드의 단일 필드를 가져올 수 있습니다. **SQLGetDescField는** ODBC에 정의된 모든 설명자 필드와 드라이버 정의 필드에 대한 응용 프로그램 액세스를 제공합니다.  
  
 **SQLGetDescRec는** 열 또는 매개 변수 데이터의 데이터 형식 및 저장소에 영향을 주는 여러 설명자 필드의 설정을 검색하기 위해 호출할 수 있습니다.
