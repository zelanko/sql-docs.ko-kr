---
title: SQLSetEnvAttr 및 커서 라이브러리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42d6804bf8a3544de44c03266ce28712e1b04d90
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300523"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 및 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 **SQLSetEnvAttr** 함수를 커서 라이브러리와 함께 사용 하는 방법을 설명 합니다. **SQLSetEnvAttr**에 대 한 일반 정보는 [SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)를 참조 하세요.  
  
 커서 라이브러리는 응용 프로그램 버전 또는 드라이버 버전과 관계 없이 SQL_ATTR_ODBC_VERSION 환경 특성 설정의 영향을 받지 않습니다.
