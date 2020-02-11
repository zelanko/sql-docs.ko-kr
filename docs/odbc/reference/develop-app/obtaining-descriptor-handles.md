---
title: 설명자 핸들 가져오기 | Microsoft Docs
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
ms.openlocfilehash: 8bfa0b36ecca3af655efde84c3ce3f22ab0c1f88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086311"
---
# <a name="obtaining-descriptor-handles"></a>설명자 핸들 얻기
응용 프로그램은 **SQLAllocHandle**에 대 한 호출의 출력 인수로 명시적으로 할당 된 설명자의 핸들을 가져옵니다. 암시적으로 할당 된 설명자의 핸들은 **SQLGetStmtAttr**를 호출 하 여 가져옵니다.
