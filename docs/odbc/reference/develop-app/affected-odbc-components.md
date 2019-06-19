---
title: ODBC 구성 요소에 영향을 받는 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72e004e6fd41ee74643fc05ec9020e6ac1933e09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186253"
---
# <a name="affected-odbc-components"></a>영향을 받는 ODBC 구성 요소
이전 버전과 호환성 드라이버 관리자의 새 버전을 도입 하 여 응용 프로그램, 드라이버 관리자 및 드라이버 영향을 설명 합니다. 이 응용 프로그램 및 드라이버 때 적용 하나 또는 둘 다 이전 버전에서 유지 됩니다. 가 따라서 세 가지 유형의 이전 버전과 호환성을 고려해 야 할 다음 표에 나와 있는 것 처럼 합니다.  
  
|형식|DM 버전|응용 프로그램의 버전|드라이버의 버전|  
|----------|-------------------|----------------------------|-----------------------|  
|드라이버 관리자의 이전 버전과 호환성|3 *.x*|2.*x*|2.*x*|  
|드라이버 [1]의 이전 버전과 호환성|3 *.x*|2.*x*|3.*x*|  
|응용 프로그램의 이전 버전과 호환성|3.*x*|3.*x*|2.*x*|  
  
 [1]의 이전 버전과 호환성 드라이버의 부록 g: 주로 설명 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
  
> [!NOTE]
>  표준 호환 응용 프로그램-예를 들어는 Open Group 또는 ISO CLI 표준에 따라 작성 된 응용 프로그램은 항상 작동을 ODBC 3 *.x* ODBC 3를 통해 드라이버 *.x*드라이버 관리자입니다. 응용 프로그램을 사용 하는 기능은 드라이버에서 사용할 수 있는 것으로 간주 합니다. 표준 호환 응용 프로그램을 ODBC 3를 사용 하 여 컴파일된에 또한 간주 *.x* 헤더 파일입니다.
