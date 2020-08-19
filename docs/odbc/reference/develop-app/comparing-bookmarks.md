---
description: 책갈피 비교
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 939c3780fc9c6738a307e9a969a346951cfac5e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476785"
---
# <a name="comparing-bookmarks"></a>책갈피 비교
책갈피는 바이트를 비교할 수 있기 때문에 같음 또는 같지 않음을 비교할 수 있습니다. 이렇게 하기 위해 응용 프로그램은 각 책갈피를 바이트 배열로 처리 하 고 두 책갈피 바이트를 비교 합니다. 책갈피는 결과 집합 내 에서만 고유 해야 하므로 다른 결과 집합에서 가져온 책갈피를 비교 하는 것은 의미가 없습니다.
