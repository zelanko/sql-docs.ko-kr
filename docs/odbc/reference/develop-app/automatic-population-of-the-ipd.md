---
title: IPD의 자동 채우기 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1591843667ef01c6c88f5dfafb734f044679b2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909836"
---
# <a name="automatic-population-of-the-ipd"></a>IPD의 자동 채우기
일부 드라이버는 매개 변수가 있는 쿼리를 준비한 후 IPD의 필드를 설정할 수 있습니다. 설명자 필드 데이터 형식, 정밀도, 배율 및 기타 특성을 포함 하 여 매개 변수에 대 한 정보를 사용 하 여 자동으로 채워집니다. 이 지원 하기 위해 동일 **SQLDescribeParam**합니다. 이 정보는 임시 쿼리 응용 프로그램에 대 한 알 수 없습니다는 매개 변수를 사용 하 여 수행 될 때와 같은 검색 후 다른 방법이 없는 경우 응용 프로그램에 특히 유용할 수 있습니다.  
  
 응용 프로그램이 드라이버를 호출 하 여 자동 채우기를 지원 하는지 여부를 결정 **SQLGetConnectAttr** 사용 하 여는 *특성* SQL_ATTR_AUTO_IPD입니다. Sql_true는 해당 반환 되 면 드라이버에서 지 원하는 및 응용 프로그램 SQL_TRUE로 SQL_ATTR_ENABLE_AUTO_IPD 문 특성을 설정 하 여 설정할 수 있습니다.  
  
 매개 변수 표식이 포함 된 SQL 문을 호출 하 여 준비 된 후 드라이버가 IPD의 필드를 채웁니다 자동 채우기를 지원 되 고 사용 하는 경우 **SQLPrepare**합니다. 응용 프로그램 호출 하 여이 정보를 검색할 수 있습니다 **SQLGetDescField** 하거나 **SQLGetDescRec**, 또는 **SQLDescribeParam**합니다. 응용 프로그램 매개 변수에 대해 가장 적합 한 응용 프로그램 버퍼를 바인딩할 또는 데이터 변환에 대 한 지정 정보를 사용할 수 있습니다.  
  
 IPD의 자동 채우기는 성능 저하가 발생할 수 있습니다. 응용 프로그램 해제할 수 (기본값) SQL_FALSE를 SQL_ATTR_ENABLE_AUTO_IPD 문 특성을 설정 하 여 합니다.
