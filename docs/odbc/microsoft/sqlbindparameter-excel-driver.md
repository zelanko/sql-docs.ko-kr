---
description: SQLBindParameter(Excel 드라이버)
title: SQLBindParameter (Excel 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLBindParameter
- SQLBindParameter function [ODBC], Excel Driver
ms.assetid: 40489bc5-3e2a-425e-892d-e0dc037f4d7a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f18d34bb17f6f6b039bac5f6842ff837c22f362
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483376"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 Microsoft Excel 드라이버를 사용 하는 경우 매개 변수를 사용 하 여 SQL_CHAR 열에 NULL을 삽입 하는 INSERT 문을 실행 하면 SQLSTATE 01004, "데이터가 잘렸습니다."와 함께 SQL_SUCCESS_WITH_INFO 반환 됩니다.
