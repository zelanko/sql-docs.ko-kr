---
title: 열 이름 제한 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281383"
---
# <a name="column-name-limitations"></a>열 이름 제한 사항
열 이름에는 모든 유효한 문자 (예: 공백)를 사용할 수 있습니다. 문자, 숫자 및 밑줄을 제외한 모든 문자가 열 이름에 포함 되어 있으면 이름을 백슬래시 (')로 묶어 구분 해야 합니다.  
  
 Microsoft Access 또는 Microsoft Excel 드라이버를 사용 하는 경우 열 이름은 64 자로 제한 되 고 긴 이름은 오류를 생성 합니다. Paradox 드라이버를 사용 하는 경우 최대 열 이름은 25 자입니다. 텍스트 드라이버를 사용 하는 경우 최대 열 이름은 64 자이 고 긴 이름은 잘립니다.  
  
 DBASE 드라이버를 사용 하는 경우 ASCII 값이 127 보다 큰 문자는 밑줄로 변환 됩니다.  
  
 Microsoft Excel 드라이버를 사용 하는 경우 열 이름이 있으면 첫 번째 행에 있어야 합니다. Microsoft Excel에서 "!" 문자를 사용 하는 이름은 백슬래시 (')로 묶어야 합니다. "!" 문자는 이름이 백슬래시 안에 포함 된 경우에도 ODBC 이름에 사용할 수 없으므로 "!" 문자는 "$" 문자로 변환 됩니다. 다른 모든 유효한 Microsoft Excel 문자 (파이프 문자 (&#124;) 제외)는 공백을 포함 하 여 열 이름에 사용할 수 있습니다. Microsoft Excel 열 이름에 공백을 포함 하려면 구분 식별자를 사용 해야 합니다. 지정 되지 않은 열 이름이 첫 번째 열에 대 한 "Col1"과 같이 드라이버 생성 이름으로 바뀝니다.  
  
 열 이름에는 파이프 문자 (&#124;)를 사용할 수 없습니다. 이름이 큰따옴표로 묶여 있는지 여부에 관계 없이 사용할 수 있습니다.  
  
 텍스트 드라이버를 사용 하는 경우 열 이름을 지정 하지 않으면 드라이버에서 기본 이름을 제공 합니다. 예를 들어 드라이버는 첫 번째 열 F1, 두 번째 열 F2 등을 호출 합니다.
