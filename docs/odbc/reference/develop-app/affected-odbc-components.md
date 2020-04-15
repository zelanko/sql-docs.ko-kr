---
title: 영향을 받는 ODBC 구성 요소 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306477"
---
# <a name="affected-odbc-components"></a>영향을 받는 ODBC 구성 요소
이전 버전과의 호환성은 응용 프로그램, 드라이버 관리자 및 드라이버가 새 버전의 드라이버 관리자도입으로 인해 영향을 받는 방식을 설명합니다. 이는 응용 프로그램 및 드라이버 중 하나 또는 둘 다 이전 버전에 남아 있을 때 영향을 줍니다. 따라서 다음 표와 같이 고려해야 할 세 가지 유형의 이전 버전과의 호환성이 있습니다.  
  
|Type|DM 버전|응용 프로그램 버전|드라이버 버전|  
|----------|-------------------|----------------------------|-----------------------|  
|드라이버 관리자의 이전 버전과의 호환성|*3.x*|*2.x*|*2.x*|  
|드라이버의 이전 버전과의 호환성[1]|*3.x*|*2.x*|*3.x*|  
|응용 프로그램의 이전 버전과의 호환성|*3.x*|*3.x*|*2.x*|  
  
 [1] 드라이버의 이전 버전과의 호환성은 주로 부록 G: 이전 버전과의 호환성에 대한 드라이버 지침에서 설명합니다.  
  
> [!NOTE]
>  개방형 그룹 또는 ISO CLI 표준에 따라 작성된 응용 프로그램과 같은 표준을 준수하는 응용 프로그램은 ODBC *3.x* 드라이버 관리자를 통해 ODBC *3.x* 드라이버와 함께 작동하도록 보장됩니다. 응용 프로그램에서 사용 하는 기능을 드라이버에서 사용할 수 있다고 가정 합니다. 또한 표준 준수 응용 프로그램이 ODBC *3.x* 헤더 파일로 컴파일된 것으로 가정합니다.
