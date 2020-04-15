---
title: IPD의 자동 채우기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1998ea1992ee7f14d87d01e348d955b017166088
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285073"
---
# <a name="automatic-population-of-the-ipd"></a>IPD의 자동 채우기
일부 드라이버는 매개 변수화된 쿼리가 준비된 후 IPD 필드를 설정할 수 있습니다. 설명자 필드는 데이터 형식, 정밀도, 배율 및 기타 특성을 포함하여 매개 변수에 대한 정보로 자동으로 채워집니다. 이는 **SQLDescribeParam을**지원하는 것과 같습니다. 이 정보는 응용 프로그램에서 알지 못하는 매개 변수로 임시 쿼리를 수행할 때와 같이 검색할 수 있는 다른 방법이 없는 경우 응용 프로그램에 특히 유용할 수 있습니다.  
  
 응용 프로그램은 드라이버가 SQL_ATTR_AUTO_IPD *특성을* 사용하여 **SQLGetConnectAttr을** 호출하여 자동 채우기를 지원하는지 여부를 결정합니다. SQL_TRUE 반환되면 드라이버는 이를 지원하며 응용 프로그램은 SQL_ATTR_ENABLE_AUTO_IPD 문 특성을 SQL_TRUE 설정하여 이를 활성화할 수 있습니다.  
  
 자동 채우기가 지원되고 활성화되면 **드라이버는 SQLPrepare**에 대한 호출을 통해 매개 변수 마커를 포함하는 SQL 문이 준비된 후 IPD 필드를 채웁니다. 응용 프로그램은 **SQLGetDescField** 또는 **SQLGetDescRec**또는 **SQLDescribeParam을**호출하여 이 정보를 검색할 수 있습니다. 응용 프로그램은 이 정보를 사용하여 매개 변수에 가장 적합한 응용 프로그램 버퍼를 바인딩하거나 매개 변수에 대한 데이터 변환을 지정할 수 있습니다.  
  
 IPD의 자동 채우기는 성능 저하를 생성할 수 있습니다. 응용 프로그램은 SQL_ATTR_ENABLE_AUTO_IPD 문 특성을 SQL_FALSE(기본값)으로 재설정하여 해제할 수 있습니다.
