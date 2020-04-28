---
title: SQLTables (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 938ceba5da25d176628d5c1d9875383d977e3aec
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299333"
---
# <a name="sqltables-text-file-driver"></a>SQLTables(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|모든 드라이버가 소유자 이름을 지원 하지 않으므로 *Sztableowner* 에 대해 올바른 인수는 NULL입니다. *Sztableowner* 를 NULL로 설정 하면 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열에서 **Sqltables** 는 디렉터리에 대 한 경로를 반환 합니다.|  
|*SzTableType*|"TABLE"은 유일 하 게 지원 되는 테이블 유형입니다.<br /><br /> 텍스트 드라이버를 사용 하는 경우 **Sqltables** 에서 반환 되는 파일 목록은 **ODBC 텍스트 설정** 대화 상자의 **확장 목록** 상자에 있는 파일 확장명에 의해 결정 됩니다.|
