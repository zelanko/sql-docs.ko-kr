---
title: 책갈피로 스크롤 | 마이크로 소프트 문서
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
ms.openlocfilehash: 454e29abdf848fdf4f4eaae090e7cc326f0048df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304194"
---
# <a name="scrolling-by-bookmark"></a>책갈피로 스크롤
**SQLFetchScroll로**행을 가져올 때 응용 프로그램은 시작 행을 선택하는 기준으로 책갈피를 사용할 수 있습니다. 이 책갈피는 현재 커서 위치를 사용하지 않기 때문에 절대 주소 형태로 되어 있습니다. 책갈피를 받는 행으로 스크롤하려면 응용 프로그램에서 SQL_FETCH_BOOKMARK *FetchOrientation을* 사용하여 **SQLFetchScroll를** 호출합니다. 이 작업은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성으로 가리키는 책갈피를 사용합니다. 이 책갈피를 통해 식별된 행부터 행 집합을 반환합니다. 응용 프로그램은 **SQLFetchScroll**에 대한 호출의 *FetchOffset* 인수에서 이 작업에 대한 오프셋을 지정할 수 있습니다. 오프셋을 지정하면 반환된 행 집합의 첫 번째 행은 *FetchOffset* 인수의 번호를 책갈피로 식별된 행 수에 추가하여 결정됩니다. ODBC 2와 함께 사용할 때 *FetchOffset* 인수의 이 사용은 지원되지 않습니다. *x* 드라이버; 응용 프로그램이 ODBC 2에서 **SQLFetchScroll를** 호출할 때 *fetchOrientationSQL_FETCH_BOOKMARK설정된* *x* 드라이버, *FetchOffset* 인수를 0으로 설정해야 합니다.
