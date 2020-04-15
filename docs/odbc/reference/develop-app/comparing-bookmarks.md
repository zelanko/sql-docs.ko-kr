---
title: 책갈피 비교 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c28392c0d48984b4aaf8a8df442b6a4054a7eced
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307478"
---
# <a name="comparing-bookmarks"></a>책갈피 비교
책갈피는 바이트와 비교할 수 있으므로 같음 또는 부등식에 대해 비교할 수 있습니다. 이렇게 하려면 응용 프로그램은 각 책갈피를 바이트 배열로 처리하고 두 개의 책갈피 바이트별 을 비교합니다. 책갈피는 결과 집합 내에서만 구별되도록 보장되므로 다른 결과 집합에서 가져온 책갈피를 비교하는 것은 의미가 없습니다.
