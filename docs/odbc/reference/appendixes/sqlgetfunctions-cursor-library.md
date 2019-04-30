---
title: SQLGetFunctions (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1123a6497207f40bd210edf35b9b4477bc9c7b6b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188732"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLGetFunctions** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLGetFunctions**를 참조 하십시오 [SQLGetFunctions 함수](../../../odbc/reference/syntax/sqlgetfunctions-function.md)합니다.  
  
 호출 하는 경우 **SQLGetFunctions**, 커서 라이브러리를 지원 하는지 반환 **SQLExtendedFetch**합니다 **SQLFetchScroll**, **SQLSetPos**, 및 **SQLSetScrollOptions**, 드라이버에서 지 원하는 함수 외에도 합니다.
