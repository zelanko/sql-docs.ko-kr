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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74e57f98b7d5e3e1508a960b342521ea5d315a3d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693491"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 및 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLSetEnvAttr** 커서 라이브러리를 사용 하 여 함수입니다. 에 대 한 일반 정보에 대 한 **SQLSetEnvAttr**를 참조 하십시오 [SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다.  
  
 커서 라이브러리를 SQL_ATTR_ODBC_VERSION 환경 특성 드라이버 버전을 응용 프로그램 버전에 관계 없이 설정의 영향을 받지 않습니다.
