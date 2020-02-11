---
title: 설명자 필드에서 값 검색 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55d7017c659ca4d0b8094ed4a665d27c10b355f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020453"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>설명자 필드에서 값 검색
응용 프로그램은 **SQLGetDescField** 를 호출 하 여 설명자 레코드의 단일 필드를 가져올 수 있습니다. **SQLGetDescField** 는 ODBC에 정의 된 모든 설명자 필드와 드라이버 정의 필드에 응용 프로그램 액세스를 제공 합니다.  
  
 **SQLGetDescRec** 을 호출 하 여 열 또는 매개 변수 데이터의 데이터 형식 및 저장소에 영향을 주는 여러 설명자 필드의 설정을 검색할 수 있습니다.
