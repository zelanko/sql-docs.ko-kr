---
title: 설명자를 암시적으로 할당 된 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d805b110453c5fe0bb5be8c8df067c09ff8146e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913878"
---
# <a name="implicitly-allocated-descriptors"></a>암시적으로 할당 된 설명자
문 핸들 할당 되 면 응용 프로그램에서 4 개의 설명자의 집합 암시적으로 할당 합니다. 응용 프로그램 문 핸들의 특성으로 설명자를 암시적으로 할당 된 이러한 핸들을 가져올 수 있습니다. 문 핸들을 해제 하는 응용 프로그램, 드라이버는 해당 핸들의 모든 암시적으로 할당 된 설명자를 해제 합니다.
