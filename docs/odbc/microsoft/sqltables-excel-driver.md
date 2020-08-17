---
description: SQLTables(Excel 드라이버)
title: SQLTables (Excel 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acedd48fb48e8f8db844feb1911f044c472006a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339649"
---
# <a name="sqltables-excel-driver"></a>SQLTables(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|모든 드라이버가 소유자 이름을 지원 하지 않으므로 *Sztableowner* 에 대해 올바른 인수는 NULL입니다. *Sztableowner* 를 NULL로 설정 하면 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|Microsoft Excel 3.0 또는 4.0 드라이버를 사용 하는 경우 기존 테이블의 이름이 아닌 *Sztablequalifier* 의 값을 사용 하 여 **sqltables** 를 호출 하면 드라이버에서 해당 이름의 테이블을 만듭니다.<br /><br /> TABLE_QUALIFIER 열에서 **Sqltables** 는 디렉터리에 대 한 경로를 반환 합니다.|  
|*SzTableType*|Microsoft Excel 3.0 또는 4.0의 경우 "TABLE"은 유일 하 게 지원 되는 테이블 유형입니다.<br /><br /> 이후 버전의 Microsoft Excel 파일에서는 시트 이름 (끝에 "$"가 있는 테이블)에 대해 "시스템 테이블"이 반환 되 고 워크시트 내의 테이블에 대해 "TABLE"이 반환 됩니다.|
