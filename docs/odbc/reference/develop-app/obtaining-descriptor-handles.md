---
title: 처리 설명자 얻기 | Microsoft Docs
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9848bf1fefed159865861ba609ec977e317094fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="obtaining-descriptor-handles"></a>처리 설명자 얻기
응용 프로그램이에 대 한 호출의 출력 인수로 모든 명시적으로 할당 된 설명자 핸들을 가져오면 **SQLAllocHandle**합니다. 호출 하 여 암시적으로 할당 된 설명자 핸들 가져옵니다 **SQLGetStmtAttr**합니다.
