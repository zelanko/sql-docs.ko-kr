---
description: SQLTransact(Access 드라이버)
title: SQLTransact (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9b00f8f5a12af2d3823171d22ad53106569352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339697"
---
# <a name="sqltransact-access-driver"></a>SQLTransact(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 Microsoft Access 드라이버를 사용 하는 경우 **Sqltransact**호출에서 *fType* 인수에 대해 SQL_COMMIT 및 SQL_ROLLBACK 지원 됩니다.  
  
 커밋 프로세스 중에 오류가 발생 하는 경우 Microsoft Access 드라이버 설정의 데이터베이스 복구 옵션을 사용 하거나 **SQLConfigDataSource** 함수에서 REPAIR_DB 키워드를 사용 하 여 영향을 받는 데이터베이스를 복구할 수 있습니다.
