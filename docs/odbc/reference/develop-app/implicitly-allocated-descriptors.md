---
description: 암시적으로 할당된 설명자
title: 암시적으로 할당 된 설명자 | Microsoft Docs
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
ms.openlocfilehash: 5daa7f622798e1394c186b333069933b48e367af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461425"
---
# <a name="implicitly-allocated-descriptors"></a>암시적으로 할당된 설명자
문 핸들이 할당 되 면 응용 프로그램은 네 개의 설명자 집합을 암시적으로 할당 합니다. 응용 프로그램은 이러한 암시적으로 할당 된 설명자의 핸들을 문 핸들의 특성으로 가져올 수 있습니다. 응용 프로그램에서 문 핸들을 해제 하면 드라이버는 해당 핸들에서 암시적으로 할당 된 모든 설명자를 해제 합니다.
