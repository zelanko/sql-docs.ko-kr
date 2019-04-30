---
title: 열 이름 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a80ed397ae494bc686ef76aaeeef10b61662f19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301807"
---
# <a name="column-name-limitations"></a>열 이름 제한 사항
열 이름 (예를 들어, 공백) 유효한 문자를 포함할 수 있습니다. 열 이름은 문자, 숫자 및 밑줄을 제외한 모든 문자가 들어 있는 경우 백 따옴표 (')에 포함 하 여 이름을 구분 해야 합니다.  
  
 Microsoft Access 또는 Microsoft Excel 드라이버를 사용 하는 열 이름은 64 자로 제한 시간과 긴 이름에 오류가 발생 합니다. Paradox 드라이버를 사용 하면 최대 열 이름은 25 자입니다. 텍스트 드라이버를 사용 하면 최대 열 이름은 64 자 및 이름이 잘립니다.  
  
 DBASE 드라이버를 사용 하면 ASCII 값이 127 보다 큰 문자는 밑줄으로 변환 됩니다.  
  
 Microsoft Excel 드라이버를 사용 하면 열 이름이 있는 경우, 첫 번째 행에 있어야 합니다. Microsoft Excel에서 사용 하는 이름을 "!" 문자를 백 (') 따옴표로 묶어야 합니다. "!" 때문에 문자 "$" 문자를 변환할는 "!" 문자 이름을 백 따옴표로 묶은 경우에 ODBC 이름에서 잘못 된 문자입니다. 다른 모든 유효한 Microsoft Excel 문자 (파이프 문자를 제외 하 고 (&#124;))에 공백을 포함 하 여 열 이름을 사용할 수 있습니다. 구분된 식별자에 공백을 포함 하는 Microsoft Excel 열 이름에 대 한 사용 되어야 합니다. 지정 되지 않은 열 이름 예를 들어, "Col1" 첫 번째 열에 대 한 드라이버에서 생성 된 이름으로 바뀝니다.  
  
 파이프 문자 (&#124;) 여부 이름을 백 따옴표에 포함 되어 있는지 여부에 열 이름을 사용할 수 없습니다.  
  
 텍스트 드라이버를 사용 하면 드라이버는 열 이름을 지정 하지 않으면 기본 이름이 제공 합니다. 예를 들어, 드라이버는 첫 번째 열 F1, F2 두 번째 열 및 등을 호출합니다.
