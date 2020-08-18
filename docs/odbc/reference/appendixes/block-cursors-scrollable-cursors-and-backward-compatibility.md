---
description: 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
title: 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46f6d3611b0a55325387f2c7723734500d48af83
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411299"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
**Sqlfetchscroll** 및 **sqlfetchscroll** 는 모두 응용 프로그램에서 호출 하는 함수 집합인 API (응용 프로그래밍 인터페이스)와 드라이버에서 구현 하는 함수 집합인 SPI (서비스 공급자 인터페이스) 사이에서 ODBC의 첫 번째 명확한 분할을 나타냅니다. 이 분할은 **Sqlfetchscroll**을 사용 하 고, 표준에 맞게 bealigned 및 **sqlfetchscroll** *를 사용 하는 odbc 2.x*와도 호환 되도록 하는 odbc 3(sp3)이 필요 *합니다*.  
  
 응용 프로그램에서 호출 하는 함수 *집합인 ODBC 2.X* API는 **sqlfetchscroll** 및 관련 문 특성을 포함 합니다. 드라이버가 구현 하는 함수 *집합인 ODBC 3.X* SPI는 **sqlfetchscroll**, **sqlfetchscroll**및 관련 된 문 특성을 포함 합니다. ODBC는 API와 SPI 사이에 이러한 분할을 공식적으로 적용 하지 않으므로 ODBC *2.x 응용 프로그램* 에서 **sqlextendedfetch** 및 관련 문 특성을 호출할 수 있습니다. 그러나 ODBC 3.x 응용 프로그램에서이 작업을 수행 하는 이유는 *없습니다.* Api 및 SPIs에 대 한 자세한 내용은 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)소개를 참조 하세요.  
  
 ODBC *3.x 응용 프로그램* 에서 블록 및 스크롤 가능 커서와 함께 사용 해야 하는 함수 및 문 특성에 대 한 자세한 내용은 [블록 커서, 스크롤 가능 커서 및 Odbc 3.x 응용 프로그램의 이전 버전과의 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)을 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버 관리자가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [드라이버가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-does.md)
