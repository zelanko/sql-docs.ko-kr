---
title: IPD 자동 채우기 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909836"
---
# <a name="automatic-population-of-the-ipd"></a>IPD의 자동 채우기
일부 드라이버는 매개 변수가 있는 쿼리를 준비한 후 IPD의 필드를 설정할 수 있습니다. 설명자 필드는 데이터 형식, 전체 자릿수, 소수 자릿수 및 기타 특성을 포함 하 여 매개 변수에 대 한 정보로 자동으로 채워집니다. 이는 **SQLDescribeParam**를 지 원하는 것과 같습니다. 응용 프로그램에서 알지 못하는 매개 변수를 사용 하 여 임시 쿼리를 수행 하는 경우와 같이이 정보는 응용 프로그램에서 다른 방법으로 검색할 수 없는 경우에 특히 유용할 수 있습니다.  
  
 응용 프로그램은 SQL_ATTR_AUTO_IPD *특성* 으로 **SQLGetConnectAttr** 를 호출 하 여 드라이버가 자동 채우기를 지원 하는지 여부를 확인 합니다. SQL_TRUE 반환 되는 경우 드라이버는이를 지원 하 고, 응용 프로그램은 SQL_ATTR_ENABLE_AUTO_IPD statement 특성을 SQL_TRUE로 설정 하 여이 기능을 사용 하도록 설정할 수 있습니다.  
  
 자동 채우기를 지원 하 고 사용 하도록 설정 하면 매개 변수 표식을 포함 하는 SQL 문이 **Sqlprepare**호출로 준비 된 후 드라이버가 IPD의 필드를 채웁니다. 응용 프로그램은 **SQLGetDescField** 또는 **SQLGetDescRec**또는 **SQLDescribeParam**를 호출 하 여이 정보를 검색할 수 있습니다. 응용 프로그램은이 정보를 사용 하 여 매개 변수에 대 한 가장 적절 한 응용 프로그램 버퍼를 바인딩하거나이에 대 한 데이터 변환을 지정할 수 있습니다.  
  
 IPD를 자동으로 채우는 경우 성능 저하가 발생할 수 있습니다. 응용 프로그램은 SQL_ATTR_ENABLE_AUTO_IPD statement 특성을 SQL_FALSE (기본값)로 다시 설정 하 여 해제할 수 있습니다.
