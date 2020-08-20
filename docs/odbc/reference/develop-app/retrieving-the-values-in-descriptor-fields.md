---
description: 설명자 필드에서 값 검색
title: 설명자 필드에서 값 검색 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2118efe58b076287dd75192de679bdb74299435
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494651"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>설명자 필드에서 값 검색
응용 프로그램은 **SQLGetDescField** 를 호출 하 여 설명자 레코드의 단일 필드를 가져올 수 있습니다. **SQLGetDescField** 는 ODBC에 정의 된 모든 설명자 필드와 드라이버 정의 필드에 응용 프로그램 액세스를 제공 합니다.  
  
 **SQLGetDescRec** 을 호출 하 여 열 또는 매개 변수 데이터의 데이터 형식 및 저장소에 영향을 주는 여러 설명자 필드의 설정을 검색할 수 있습니다.
