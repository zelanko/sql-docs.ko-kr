---
title: 책갈피 비교 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44da652ad1e52934fa48f32b1b2f88b30212ad3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083301"
---
# <a name="comparing-bookmarks"></a>책갈피 비교
책갈피는 바이트를 비교할 수 있기 때문에 같음 또는 같지 않음을 비교할 수 있습니다. 이렇게 하기 위해 응용 프로그램은 각 책갈피를 바이트 배열로 처리 하 고 두 책갈피 바이트를 비교 합니다. 책갈피는 결과 집합 내 에서만 고유 해야 하므로 다른 결과 집합에서 가져온 책갈피를 비교 하는 것은 의미가 없습니다.
