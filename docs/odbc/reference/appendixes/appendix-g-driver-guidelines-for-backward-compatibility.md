---
description: '부록 G: 이전 버전과의 호환성을 위한 드라이버 지침'
title: '부록 G: 이전 버전과의 호환성을 위한 드라이버 지침 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2c09485879c2f0d16518dcfc0a17f4bf3a13943
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411409"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>부록 G: 이전 버전과의 호환성을 위한 드라이버 지침
이 부록에서는 ODBC 3에서 작동 하는 드라이버 작성자를 위한 정보를 제공 합니다. ODBC 2를 지원 해야 하는 *x* 드라이버. *x* 응용 프로그램. 이전 버전과의 호환성에 대 한 자세한 내용은 [이전 버전과의 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)를 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Odbc 3.X 드라이버의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) -새 기능은 odbc 3에 존재 하는 기능입니다. ODBC 2가 아닌 *x* *x*. ODBC 3. *x* 드라이버는 일반적으로 ODBC 2 때문에 새로운 기능과의 호환성에 대해 걱정 하지 않아도 됩니다. *x* 응용 프로그램은 사용 하지 않습니다. 이에 대 한 유일한 예외는 **Sqlfetch**, **sqlfetchscroll**, **SQLSetPos**및 **sqlextendedfetch**와 관련 된 기능입니다. 자세한 내용은이 부록의 뒷부분에 나오는을 참조 하세요.  
  
-   [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) -중복 기능은 ODBC 3에서 다르게 구현 되는 기능입니다. *x* 및 ODBC 2. *x*. ODBC 3. *x* 드라이버는 항상 ODBC 2를 매핑하기 때문에 중복 된 기능과의 호환성을 걱정 하지 않아도 됩니다. *x* 는 ODBC 3에 기능을 제공 합니다. *x* 는 ODBC 3을 호출할 때 기능을 제공 합니다. *x* 드라이버. 따라서 ODBC 3. *x* 드라이버는 ODBC 3만 봅니다. *x* 기능. 이러한 매핑에 대 한 자세한 내용은이 부록의 뒷부분에 나오는을 참조 하세요.  
  
-   동작 [변경 내용 및 odbc 3.X 드라이버](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) -동작 변경 내용은 odbc 3에서 다르게 처리 되는 기능입니다. *x* 및 ODBC 2. *x*. ODBC 3. *x* 드라이버는 동작 변경에 대해 걱정 하 고 응용 프로그램에 의해 설정 된 SQL_ATTR_ODBC_VERSION 환경 특성에 대 한 응답으로 작동 해야 합니다.
