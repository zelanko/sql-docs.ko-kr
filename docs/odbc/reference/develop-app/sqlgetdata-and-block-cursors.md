---
description: SQLGetData 및 블록 커서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53358b2d4d8dfef1a5a820ed3943f07a584a595
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424495"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 및 블록 커서
**SQLGetData** 는 단일 행의 단일 열에서 작동 하며 여러 행의 데이터를 포함 하는 배열을 인출할 수 없습니다. 이는 기본 **SQLGetData** 를 사용 하 여 파트에서 긴 데이터를 가져오는 것이 고, 한 번에 둘 이상의 행에 대해이 작업을 수행 하는 이유는 거의 발생 하지 않기 때문입니다.  
  
 블록 커서와 함께 **SQLGetData** 를 사용 하기 위해 응용 프로그램은 먼저 **SQLSetPos** 를 호출 하 여 커서를 단일 행에 배치 합니다. 그런 다음 해당 행의 열에 대해 **SQLGetData** 를 호출 합니다. 그러나이 동작은 선택 사항입니다. 드라이버가 블록 커서와의 **SQLGetData** 사용을 지원 하는지 확인 하기 위해 응용 프로그램은 SQL_GETDATA_EXTENSIONS 옵션으로 **SQLGetInfo** 를 호출 합니다.
