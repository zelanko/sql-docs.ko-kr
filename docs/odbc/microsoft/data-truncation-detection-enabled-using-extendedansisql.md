---
title: 확장AnsiSQL을 사용하여 데이터 잘림 감지 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280703"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>ExtendedAnsiSQL을 사용하여 활성화된 데이터 잘림 검색
ExtendedAnsiSQL 플래그가 켜져 있고 응용 프로그램이 char 또는 이진 열에 데이터를 삽입하고 데이터가 잘리면 잘림이 감지됩니다. ExtendedAnsiSQL 플래그가 꺼지면 ODBC 데스크톱 데이터베이스 드라이버의 이전 버전과 마찬가지로 데이터가 경고 없이 잘립니다.
