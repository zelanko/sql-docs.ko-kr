---
title: 열 이름 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41d973afdac360af114da41620997cad23a2c740
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281383"
---
# <a name="column-name-limitations"></a>열 이름 제한 사항
열 이름에는 유효한 문자(예: 공백)가 포함될 수 있습니다. 열 이름에 문자, 숫자 및 밑줄을 제외한 문자가 포함된 경우 이름을 다시 따옴표(')로 둘러싸서 이름을 구분해야 합니다.  
  
 Microsoft Access 또는 Microsoft Excel 드라이버를 사용하면 열 이름이 64자로 제한되고 이름이 길수록 오류가 발생합니다. 역설 드라이버를 사용할 때 최대 열 이름은 25자입니다. Text 드라이버를 사용하면 최대 열 이름은 64자이고 더 긴 이름은 잘립니다.  
  
 dBASE 드라이버를 사용하면 ASCII 값이 127보다 큰 문자가 밑줄로 변환됩니다.  
  
 Microsoft Excel 드라이버를 사용할 때 열 이름이 있는 경우 첫 번째 행에 있어야 합니다. Microsoft Excel에서 "!" 문자를 사용하는 이름은 뒷따옴표(')에 동봉되어야 합니다. "!" 문자는 "$" 문자로 변환되는데, 이는 "!" 문자가 ODBC 이름으로 합법적이지 않기 때문입니다. 다른 모든 유효한 Microsoft Excel 문자(파이프 문자(&#124;)를 제외한)는 공백을 포함하여 열 이름으로 사용할 수 있습니다. 공백을 포함하려면 Microsoft Excel 열 이름에 구분된 식별자를 사용해야 합니다. 지정되지 않은 열 이름은 첫 번째 열의 "Col1"과 같은 드라이버 생성 이름으로 바뀝니다.  
  
 파이프 문자(&#124;)는 이름이 따옴표로 동봉되어 있는지 여부에 관계없이 열 이름에 사용할 수 없습니다.  
  
 Text 드라이버를 사용하면 열 이름을 지정하지 않은 경우 드라이버가 기본 이름을 제공합니다. 예를 들어 드라이버는 첫 번째 열 F1, 두 번째 열 F2 등을 호출합니다.
