---
title: "설명자를 암시적으로 할당 된 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0746c31b05302eba9cd1fcf4104336ca139b6938
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="implicitly-allocated-descriptors"></a>암시적으로 할당 된 설명자
문 핸들 할당 되 면 응용 프로그램에서 4 개의 설명자의 집합 암시적으로 할당 합니다. 응용 프로그램 문 핸들의 특성으로 설명자를 암시적으로 할당 된 이러한 핸들을 가져올 수 있습니다. 문 핸들을 해제 하는 응용 프로그램, 드라이버는 해당 핸들의 모든 암시적으로 할당 된 설명자를 해제 합니다.
