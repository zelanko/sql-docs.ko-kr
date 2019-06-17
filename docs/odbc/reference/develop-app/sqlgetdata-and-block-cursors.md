---
title: SQLGetData 및 블록 커서 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a14c98f045fd974b404209cc998496dc5fa7193e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149080"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 및 블록 커서
**SQLGetData** 단일 행의 단일 열에서 작동 하 고 여러 행의 데이터를 포함 하는 배열을 가져올 수 없습니다. 주 사용 하기 때문에 이것이 **SQLGetData** 부분에서 긴 데이터를 인출 하는 것 이며 한 번에 둘 이상의 행에 대해 이렇게 하는 거의 또는 전혀 이유입니다.  
  
 사용 하 **SQLGetData** 블록 커서를 사용 하 여 응용 프로그램이 먼저 호출 **SQLSetPos** 단일 행에 커서를 배치 합니다. 그런 다음 호출 **SQLGetData** 해당 행의 열에 대 한 합니다. 그러나이 동작은 선택 사항입니다. 드라이버의 사용을 지원 하는지 확인할 **SQLGetData** 블록 커서를 사용 하 여 응용 프로그램 호출 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 옵션을 사용 하 여 합니다.
