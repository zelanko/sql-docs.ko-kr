---
title: ODBC 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 046ec16827e46f6cdf71881ec2f1b6c908fb42fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910138"
---
# <a name="affected-odbc-components"></a>영향을 받는 ODBC 구성 요소
이전 버전과 호환성 새 버전의 드라이버 관리자를 도입 하 여 응용 프로그램, 드라이버 관리자 및 드라이버 영향을 설명 합니다. 하나 또는 둘 모두에서 이전 버전에 유지 하는 경우 응용 프로그램 및 드라이버가 결정 됩니다. 세 종류가 있습니다, 따라서 이전 버전과의 호환성을 고려 하는 다음 표에 나와 있는 것 처럼 합니다.  
  
|형식|DM의 버전|응용 프로그램의 버전|드라이버의 버전|  
|----------|-------------------|----------------------------|-----------------------|  
|드라이버 관리자의 이전 버전과 호환성|3 *.x*|2.*x*|2.*x*|  
|드라이버 [1]의 이전 버전과 호환성|3 *.x*|2.*x*|3.*x*|  
|응용 프로그램의 이전 버전과 호환성|3.*x*|3.*x*|2.*x*|  
  
 [주로 이전 버전과 호환성에 대 한 드라이버의 이전 버전과 호환성 1]의 부록 g: 드라이버 지침에서 설명 합니다.  
  
> [!NOTE]  
>  표준 호환 응용 프로그램-예를 들어 하는 응용 프로그램 그룹 열기 또는 CLI ISO 표준에 따라 작성 된-은 항상 ODBC 3 작동 *.x* ODBC 3를 통해 드라이버 *.x*드라이버 관리자입니다. 응용 프로그램을 사용 하 여 기능은 드라이버에서 사용할 수 있는 것으로 간주 합니다. 표준 호환 응용 프로그램에 컴파일된 ODBC 3과 함께 가정 *.x* 헤더 파일입니다.
