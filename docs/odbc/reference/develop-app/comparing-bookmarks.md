---
title: 책갈피를 비교 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44561e4386353ef1efaf3dd41e5a24b93941963d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="comparing-bookmarks"></a>책갈피를 비교
책갈피는 비교할 수 바이트 이기 때문에 같음 또는 같지 않음을 비교할 수 있습니다. 이렇게 하려면 응용 프로그램 책갈피 마다 바이트를 배열로 처리 하 고 두 개의 책갈피-바이트를 비교 합니다. 책갈피 보장 되는 결과 집합 내 에서만 고유, 때문에 것은 다양 한 결과 집합에서 얻은 책갈피를 비교 하는 의미가 없습니다.
