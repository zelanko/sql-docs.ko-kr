---
title: 커서 라이브러리 작업 | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0bac09cb2b45274a5589c152a5b0e714b71f8dc1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-library-operations"></a>커서 라이브러리 작업
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 2를 사용 하는 응용 프로그램*.x* 드라이버에서는 ODBC 3를 호출 합니다. *x* 커서 라이브러리를 응용 프로그램 ODBC 3을 사용 하 여 할 수 있습니다. *x* ODBC 2에서 지원 되지 않는 기능*.x* 드라이버입니다. 그러나 이러한 기능을 사용 방법, 응용 프로그램 작성기에서 주의 해야 해야 합니다. ODBC 3 사용 합니다. *x* 커서 라이브러리는 ODBC 2 있도록 하지는 않지만*.x* 드라이버는 ODBC 3. *x* 드라이버입니다.
