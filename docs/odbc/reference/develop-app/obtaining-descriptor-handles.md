---
description: 설명자 핸들 얻기
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c46ce0bff7240c121c6c56a5c3cd1b19769afb04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429205"
---
# <a name="obtaining-descriptor-handles"></a>설명자 핸들 얻기
응용 프로그램은 **SQLAllocHandle**에 대 한 호출의 출력 인수로 명시적으로 할당 된 설명자의 핸들을 가져옵니다. 암시적으로 할당 된 설명자의 핸들은 **SQLGetStmtAttr**를 호출 하 여 가져옵니다.
