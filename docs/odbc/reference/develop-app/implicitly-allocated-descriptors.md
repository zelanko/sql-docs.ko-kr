---
title: 암시적으로 할당된 설명자 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 271d479a9d2faa8cd7ab01e02e830b194c4138b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300133"
---
# <a name="implicitly-allocated-descriptors"></a>암시적으로 할당된 설명자
명령문 핸들이 할당되면 응용 프로그램은 4개의 설명자 중 하나의 집합을 암시적으로 할당합니다. 응용 프로그램은 문 핸들의 특성으로 암시적으로 할당된 이러한 설명자의 핸들을 가져올 수 있습니다. 응용 프로그램이 명령문 핸들을 해제하면 드라이버는 해당 핸들에 암시적으로 할당된 모든 설명자가 해제됩니다.
