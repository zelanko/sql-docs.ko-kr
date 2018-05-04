---
title: 책갈피로 스크롤 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 823929a98b3fc7b016f8bc1dc3fa1c2ed982b9c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="scrolling-by-bookmark"></a>책갈피로 스크롤
행을 인출할 때 **SQLFetchScroll**, 응용 프로그램 시작 행을 선택 하기 위한 기반으로 한 책갈피를 사용할 수 있습니다. 이 책갈피는 현재 커서 위치를 사용하지 않기 때문에 절대 주소 형태로 되어 있습니다. 책갈피가 표시 된 행을 호출 하 여 응용 프로그램으로 스크롤해야 **SQLFetchScroll** 와 *FetchOrientation* 에서는 SQL_FETCH_BOOKMARK의 합니다. 이 작업은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에서 가리키는 책갈피를 사용 합니다. 이 책갈피를 통해 식별된 행부터 행 집합을 반환합니다. 응용 프로그램에이 작업에 대 한 오프셋을 지정할 수는 *FetchOffset* 에 대 한 호출의 인수 **SQLFetchScroll**합니다. 오프셋을 지정 하는 경우 반환된 된 행 집합의 첫 번째 행 번호에 추가 하 여 결정 됩니다는 *FetchOffset* 책갈피로 식별 된 행의 수는 인수입니다. 이러한를 사용이 하 여 *FetchOffset* ODBC 2와 함께 사용할 경우에 인수가 지원 되지 않습니다. *x* 드라이버; 응용 프로그램 호출 하는 경우 **SQLFetchScroll** ODBC 2에서. *x* 드라이버와 함께 *FetchOrientation* SQL_FETCH_BOOKMARK로 설정 된 *FetchOffset* 인수는 0으로 설정 해야 합니다.
