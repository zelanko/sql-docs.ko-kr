---
title: SQLSetEnvAttr 및 커서 라이브러리 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300523"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 및 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리와 **함께 SQLSetEnvAttr** 함수의 사용에 대해 설명합니다. **SQLSetEnvAttr에**대한 일반적인 정보는 [SQLSetEnvAttr 함수를](../../../odbc/reference/syntax/sqlsetenvattr-function.md)참조하십시오.  
  
 커서 라이브러리는 응용 프로그램 버전 이나 드라이버 버전에 관계 없이 SQL_ATTR_ODBC_VERSION 환경 특성의 설정에 의해 영향을 받지 않습니다.
