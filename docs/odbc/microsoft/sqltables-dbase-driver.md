---
title: SQLTables (dBASE 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLTables
- SQLTables function [ODBC], dBASE Driver
ms.assetid: 45938efb-b678-47d8-9345-644fa26ad679
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c31c0995c6516c68cebb7fb0e2ec374c36923f2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqltables-dbase-driver"></a>SQLTables (dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|인수|설명|  
|--------------|--------------|  
|*szTableOwner*|에 대 한 유효한 인수 *szTableOwner* 드라이버 중 소유자 이름을 지원 하기 때문에 NULL입니다. 와 *szTableOwner* NULL로 설정 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열에서 **SQLTables** 디렉터리 경로 반환 합니다.|  
|*SzTableType*|DBASE 파일에 대 한 "TABLE"은 테이블 유형만 지원 합니다.|
