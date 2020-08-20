---
description: SQLTables(Visual FoxPro ODBC 드라이버)
title: SQLTables (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 089208ab612984283e3f87c4ad03aca0ccfa2b38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471555"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 **Sqltables** 문의 매개 변수로 지정 된 테이블 이름의 목록을 반환 합니다. 매개 변수를 지정 하지 않으면 현재 데이터 소스에 저장 된 테이블 이름을 반환 합니다. 드라이버는 정보를 결과 집합으로 반환 합니다.  
  
 열거형 형식 호출은 원격 뷰 또는 로컬 매개 변수가 있는 뷰에 대 한 결과 집합 항목을 받지 않습니다. 그러나 고유 테이블 이름 지정자를 사용 하 여 **Sqltables** 를 호출 하면 해당 이름과 함께 있는 경우 해당 뷰의 일치 항목을 찾을 수 있습니다. 이를 통해 API를 사용 하 여 새 테이블을 만들기 전에 이름 충돌을 확인할 수 있습니다.  
  
> [!NOTE]  
>  Visual FoxPro ODBC 드라이버는 두 유형의 테이블이 모두 시스템의 동일한 디렉터리에 저장 되는 경우에도 [데이터베이스 테이블과](../../odbc/microsoft/visual-foxpro-terminology.md) [자유 테이블](../../odbc/microsoft/visual-foxpro-terminology.md)을 구분 합니다. 데이터 원본이 자유 테이블의 디렉터리인 경우 Visual FoxPro ODBC 드라이버는 데이터베이스와 연결 된 테이블의 이름을 카탈로그로 하거나 반환 하지 않습니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*의 [sqltables](../../odbc/reference/syntax/sqltables-function.md) 를 참조 하십시오.
