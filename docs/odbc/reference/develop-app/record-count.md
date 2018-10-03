---
title: Record Count | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f8b0a6fc7aa5765d9373af33ab4fac0a4a07aac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610433"
---
# <a name="record-count"></a>Record Count
설명자의 SQL_DESC_COUNT 헤더 필드는 데이터를 포함 하는 번호가 가장 큰 레코드의 1부터 시작 인덱스입니다. 이 필드는 모든 열 또는 바인딩되는 매개 변수 수가 없습니다. 설명자 할당 되 면 SQL_DESC_COUNT의 초기 값은 0입니다.  
  
 드라이버를 할당 하 고 설명자 정보를 저장 하는 데 필요한 저장소를 유지 관리 하는 데 필요한 모든 작업을 수행 합니다. 응용 프로그램이 명시적으로 설명자의 크기를 지정 하지 않고 새 레코드를 할당 합니다. 일수가 SQL_DESC_COUNT 값 보다 크면 설명자 레코드에 대 한 정보를 제공 하는 응용 프로그램, 드라이버 SQL_DESC_COUNT 자동으로 증가 합니다. 응용 프로그램에는 번호가 가장 높은 설명자 레코드 바인딩 해제, 드라이버 SQL_DESC_COUNT 가장 높은 나머지 바인딩된 레코드의 번호를 포함 하도록 자동으로 줄어듭니다.
