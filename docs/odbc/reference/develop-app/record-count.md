---
title: 레코드 수 | Microsoft Docs
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
ms.openlocfilehash: d4d684fb6d9614defdca3897c53c4bae9fc231a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138078"
---
# <a name="record-count"></a>Record Count
설명자의 SQL_DESC_COUNT 헤더 필드는 데이터를 포함 하는 가장 번호가 매겨진 레코드의 인덱스 (1부터 수)입니다. 이 필드는 바인딩된 모든 열 또는 매개 변수의 개수가 아닙니다. 설명자가 할당 될 때 SQL_DESC_COUNT의 초기 값은 0입니다.  
  
 드라이버는 설명자 정보를 저장 하는 데 필요한 모든 저장소를 할당 하 고 유지 관리 하는 데 필요한 모든 작업을 수행 합니다. 응용 프로그램은 설명자의 크기를 명시적으로 지정 하거나 새 레코드를 할당 하지 않습니다. 응용 프로그램에서 숫자가 SQL_DESC_COUNT 값 보다 큰 설명자 레코드에 대 한 정보를 제공 하는 경우 드라이버가 자동으로 SQL_DESC_COUNT 증가 합니다. 응용 프로그램에서 번호가 가장 높은 설명자 레코드를 바인딩 해제 하는 경우 드라이버는 남은 나머지 바인딩된 레코드 수를 포함 하도록 SQL_DESC_COUNT를 자동으로 줄입니다.
