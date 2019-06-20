---
title: 설명자를 암시적으로 할당 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa25e99c5bc0b0a5799cfac479e97bd9b89db338
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447237"
---
# <a name="implicitly-allocated-descriptors"></a>암시적으로 할당된 설명자
문 핸들 할당 될 때 응용 프로그램 4 설명자의 집합을 암시적으로 할당 합니다. 응용 프로그램의 문 핸들의 특성으로 설명자를 암시적으로 할당 된 이러한 핸들을 가져올 수 있습니다. 문 핸들 해제 하는 응용 프로그램, 드라이버는 핸들의 모든 암시적으로 할당 된 설명자를 해제 합니다.
