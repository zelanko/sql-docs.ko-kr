---
title: 영향을 받는 ODBC 구성 요소 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d9155fa1c9df5846f069e93a3db1b969e9219ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306477"
---
# <a name="affected-odbc-components"></a>영향을 받는 ODBC 구성 요소
이전 버전과의 호환성에서는 새 버전의 드라이버 관리자를 도입 하 여 응용 프로그램, 드라이버 관리자 및 드라이버의 영향을 받는 방법을 설명 합니다. 이는 둘 중 하나 또는 둘 모두가 이전 버전에 유지 되는 경우 응용 프로그램 및 드라이버에 영향을 줍니다. 따라서 다음 표에 표시 된 것 처럼 세 가지 유형의 이전 버전과의 호환성을 고려해 야 합니다.  
  
|유형|DM의 버전|응용 프로그램 버전|드라이버 버전|  
|----------|-------------------|----------------------------|-----------------------|  
|드라이버 관리자의 이전 버전과의 호환성|*3.x*|*2.x*|*2.x*|  
|[1] 드라이버의 이전 버전과의 호환성|*3.x*|*2.x*|*3.x*|  
|응용 프로그램의 이전 버전과의 호환성|*3.x*|*3.x*|*2.x*|  
  
 [1] 이전 버전과의 호환성을 위한 부록 G: 드라이버 지침에서 주로 다룹니다.  
  
> [!NOTE]
>  표준 규격 응용 프로그램 (예: 오픈 그룹 또는 ISO CLI 표준에 따라 작성 된 응용 프로그램)은 ODBC *3.x 드라이버 관리자를 통해 odbc 3.x* *드라이버에서* 작동 하도록 보장 됩니다. 응용 프로그램에서 사용 하는 기능을 드라이버에서 사용할 수 있다고 가정 합니다. 또한 표준 규격 응용 프로그램이 ODBC 2.x 헤더 파일을 사용 하 여 컴파일된 것으로 *가정 합니다.*
