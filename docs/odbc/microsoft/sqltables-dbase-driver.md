---
description: SQLTables(dBASE 드라이버)
title: SQLTables (dBASE 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLTables
- SQLTables function [ODBC], dBASE Driver
ms.assetid: 45938efb-b678-47d8-9345-644fa26ad679
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cadded2fe1dfdcb99902a69bb5cbc0608b4614e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339899"
---
# <a name="sqltables-dbase-driver"></a>SQLTables(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|모든 드라이버가 소유자 이름을 지원 하지 않으므로 *Sztableowner* 에 대해 올바른 인수는 NULL입니다. *Sztableowner* 를 NULL로 설정 하면 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열에서 **Sqltables** 는 디렉터리에 대 한 경로를 반환 합니다.|  
|*SzTableType*|DBASE 파일의 경우 "TABLE"은 유일 하 게 지원 되는 테이블 형식입니다.|
