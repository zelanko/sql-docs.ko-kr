---
title: SQLGetData 및 블록 커서 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8642e5c228bb0e7976099d2151fe36f4db683f27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 및 블록 커서
**SQLGetData** 단일 행의 단일 열에서 작동 하 고 여러 행에서에서 데이터를 포함 하는 배열을 가져올 수 없습니다. 기본 사용 하기 때문에 이것이 **SQLGetData** 부분으로 긴 데이터를 인출 하는 것 이며 한 번에 둘 이상의 행에 대 한 할 거의 없거나 전혀 없이 이유입니다.  
  
 사용 하도록 **SQLGetData** 블록 커서와 함께 응용 프로그램 먼저 호출 **SQLSetPos** 단일 행에 커서를 배치 하 합니다. 그런 다음 연속 호출 **SQLGetData** 같은 행의 열에 대 한 합니다. 그러나이 문제는 선택 사항입니다. 드라이버의 사용을 지원 하는지 확인 하 **SQLGetData** 응용 프로그램 블록 커서와 함께 호출 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 옵션을 사용 합니다.
