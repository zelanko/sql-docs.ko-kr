---
title: 열 이름 제한 | Microsoft Docs
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
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f3f384b9a2080ab683c8148effe7c6a9a13fcd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="column-name-limitations"></a>열 이름 제한 사항
열 이름은 유효한 모든 문자 (예: 공백)을 포함할 수 있습니다. 열 이름은 문자, 숫자 및 밑줄을 제외한 모든 문자가 들어 있으면 역 따옴표 (')에 포함 하 여 이름을 구분 해야 합니다.  
  
 Microsoft Access 또는 Microsoft Excel 드라이버를 사용 하면 열 이름은 64 자로 제한 되며 및 긴 이름을 오류를 생성 합니다. Paradox 드라이버를 사용 하면 최대 열 이름은 25 자입니다. 텍스트 드라이버를 사용 하면 최대 열 이름이 64 자가 고 긴 이름이 잘립니다.  
  
 DBASE 드라이버를 사용 하는 경우 밑줄 문자는 ASCII 값이 127 보다 큰 변환 됩니다.  
  
 Microsoft Excel 드라이버를 사용 하면 열 이름이 있는 경우, 첫 번째 행에 있어야 합니다. Microsoft Excel에서 사용 하는 이름에서 "!" 문자를 뒤로 따옴표 (')에 포함 되어야 합니다. "!" 때문에 문자 "$" 문자 변환할는 "!"는 이름이 백 따옴표로 묶여 있는 경우에 문자는 ODBC 이름에 올바르지 않습니다. 다른 모든 유효한 Microsoft Excel 문자 (파이프 문자를 제외 하 고 (&#124;))에 공백을 포함 하 여 열 이름을 사용할 수 있습니다. 공백을 포함 하는 Microsoft Excel 열 이름에 대 한 구분된 식별자를 따라야 합니다. 지정 되지 않은 열 이름은 드라이버에서 생성 된 이름으로, 예를 들어 "Col1" 첫 번째 열에 대 한 대체 됩니다.  
  
 파이프 문자 (&#124;) 이름을 따옴표로 백 아닌지 여부를 열 이름에 사용할 수 없습니다.  
  
 텍스트 드라이버를 사용 하면 드라이버는 열 이름을 지정 하지 않으면 기본 이름이 제공 합니다. 예를 들어 첫 번째 열 F1, F2, 두 번째 열 등에 드라이버를 호출합니다.
