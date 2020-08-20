---
description: 책갈피로 스크롤
title: 책갈피로 스크롤 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52ef0813f3f9fd3f2d139a2549000c629943109e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476475"
---
# <a name="scrolling-by-bookmark"></a>책갈피로 스크롤
**Sqlfetchscroll**을 사용 하 여 행을 인출 하는 경우 응용 프로그램은 시작 행을 선택 하기 위한 기준으로 책갈피를 사용할 수 있습니다. 이 책갈피는 현재 커서 위치를 사용하지 않기 때문에 절대 주소 형태로 되어 있습니다. 책갈피가 설정 된 행으로 스크롤하려면 응용 프로그램은 SQL_FETCH_BOOKMARK의 *Fetchorientation* 로 **sqlfetchscroll** 을 호출 합니다. 이 작업은 SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성에 의해 가리키는 책갈피를 사용 합니다. 이 책갈피를 통해 식별된 행부터 행 집합을 반환합니다. 응용 프로그램은 **Sqlfetchscroll**에 대 한 호출의 *fetchoffset* 인수에서이 작업에 대 한 오프셋을 지정할 수 있습니다. 오프셋이 지정 된 경우 반환 된 행 집합의 첫 번째 행은 *Fetchoffset* 인수에서 책갈피에 의해 식별 된 행 수에 숫자를 더하여 결정 됩니다. 이러한 *Fetchoffset* 인수 사용은 ODBC 2와 함께 사용할 경우 지원 되지 않습니다. *x* 드라이버 응용 프로그램이 ODBC 2에서 **Sqlfetchscroll** 을 호출 하는 경우 *Fetchorientation* 가 SQL_FETCH_BOOKMARK로 설정 된 *x* 드라이버는 *fetchorientation* 인수를 0으로 설정 해야 합니다.
