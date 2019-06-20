---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90ba6ed3a6feb163fbe1eaf39cce14ae501c232e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468379"
---
# <a name="scrolling-by-bookmark"></a>책갈피로 스크롤
사용 하 여 행을 인출할 때 **SQLFetchScroll**, 응용 프로그램 시작 행을 선택 하기 위한 기초로 책갈피에 사용할 수 있습니다. 이 책갈피는 현재 커서 위치를 사용하지 않기 때문에 절대 주소 형태로 되어 있습니다. 책갈피가 표시 된 행을 호출 하 여 응용 프로그램으로 스크롤해야 **SQLFetchScroll** 사용 하 여를 *FetchOrientation* 에서는 SQL_FETCH_BOOKMARK의 합니다. 이 작업은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성이 가리키는 책갈피를 사용 합니다. 이 책갈피를 통해 식별된 행부터 행 집합을 반환합니다. 응용 프로그램에서이 작업에 대 한 오프셋을 지정할 수는 *FetchOffset* 에 대 한 호출의 인수 **SQLFetchScroll**합니다. 오프셋을 지정 하는 경우 반환된 된 행 집합의 첫 번째 행의 수를 추가 하 여 결정 됩니다 합니다 *FetchOffset* 인수에 책갈피를 통해 식별 된 행의 개수입니다. 이 사용 된 *FetchOffset* 인수에는 ODBC 2를 사용 하는 경우 지원 되지 않습니다. *x* 드라이버, 응용 프로그램을 호출할 때 **SQLFetchScroll** 는 ODBC 2. *x* 드라이버와 함께 *FetchOrientation* SQL_FETCH_BOOKMARK로 설정 합니다 *FetchOffset* 인수는 0으로 설정 되어 있어야 합니다.
