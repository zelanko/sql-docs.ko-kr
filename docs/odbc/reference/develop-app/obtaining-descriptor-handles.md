---
title: 설명자 핸들 얻기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 983097de95e41914bb4d577cb071d790a795f96d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254683"
---
# <a name="obtaining-descriptor-handles"></a>설명자 핸들 얻기
응용 프로그램에 대 한 호출의 출력 인수로 명시적으로 할당 된 설명자 핸들을 가져옵니다 **SQLAllocHandle**합니다. 암시적으로 할당 된 설명자 핸들을 호출 하 여 가져온 **SQLGetStmtAttr**합니다.
