---
title: 유니코드 드라이버 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284355"
---
# <a name="unicode-drivers"></a>유니코드 드라이버
드라이버가 유니코드 드라이버여야 하는지 ANSI 드라이버인지여부는 전적으로 데이터 원본의 특성에 따라 달라집니다. 데이터 원본이 유니코드 데이터를 지원하는 경우 드라이버는 유니코드 드라이버여야 합니다. 데이터 원본이 ANSI 데이터만 지원하는 경우 드라이버는 ANSI 드라이버로 남아 있어야 합니다.  
  
 유니코드 드라이버는 드라이버 관리자에서 유니코드 드라이버로 인식하려면 **SQLConnectW를** 내보내야 합니다.  
  
 유니코드 드라이버는 유니코드 *함수(W*의 접미사)를 수락하고 유니코드 데이터를 저장해야 합니다. 또한 ANSI 함수를 허용할 수 있지만 필요하지는 않습니다. 드라이버 관리자는 *A* 접미사가 있는 ANSI 함수 호출을 드라이버에 전달하지 않지만 접미사 없이 ANSI 함수 호출로 변환한 다음 드라이버에 전달합니다.  
  
 유니코드 드라이버는 응용 프로그램의 바인딩에 따라 유니코드 또는 ANSI로 결과 집합을 반환할 수 있어야 합니다. 응용 프로그램이 SQL_C_CHAR 바인딩하는 경우 유니코드 드라이버는 SQL_WCHAR 데이터를 SQL_CHAR 변환해야 합니다. 드라이버 관리자는 anSI 드라이버에 대해 SQL_C_CHAR SQL_C_WCHAR 매핑하지만 유니코드 드라이버에 대한 매핑은 수행하지 않습니다.  
  
> [!NOTE]  
>  드라이버 유형을 결정할 때 드라이버 관리자는 **SQLSetConnectAttr을** 호출하고 연결 시 SQL_ATTR_ANSI_APP 특성을 설정합니다. 응용 프로그램이 ANSI API를 사용하는 경우 SQL_ATTR_ANSI_APP SQL_AA_TRUE 설정되고 유니코드를 사용하는 경우 SQL_AA_FALSE 값으로 설정됩니다. 이 특성은 드라이버가 응용 프로그램 유형에 따라 다른 동작을 나타낼 수 있도록 사용됩니다. 응용 프로그램에서 직접 특성을 설정할 수 없으며 **SQLGetConnectAttr**에서 지원되지 않습니다. 드라이버가 ANSI 및 유니코드 응용 프로그램 모두에 대해 동일한 동작을 나타내는 경우 이 특성에 대해 SQL_ERROR 반환해야 합니다. 드라이버가 SQL_SUCCESS 반환하는 경우 드라이버 관리자는 연결 풀링을 사용할 때 ANSI 및 유니코드 연결을 분리합니다.
