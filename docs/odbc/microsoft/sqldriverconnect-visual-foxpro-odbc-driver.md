---
title: SQLDriverConnect (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc0bcf6a191f67b87b422b17778f56feda1f5227
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238085"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 일 수 있는 기존 데이터 원본에 연결 하는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 의 디렉터리나 [테이블 무료](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. UID 및 PWD ODBC 특성 키워드는 무시 됩니다. 다음 표에서 지원 되는 추가 특성 키워드를 나열합니다.  
  
|ODBC 특성 키워드|특성 값|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC 드라이버에서 무시 되지만 오류를 생성 하지 않습니다.|  
|PWD|Visual FoxPro ODBC 드라이버에서 무시 되지만 오류를 생성 하지 않습니다.|  
|드라이버|이름과 위치의 Visual FoxPro ODBC 드라이버. 드라이버 관리자에 의해 구현 됩니다.|  
  
|Visual FoxPro ODBC 드라이버 특성 키워드|특성 값|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Yes" 또는 "No"|  
|한 부씩 인쇄|"컴퓨터" 또는 다른 데이터 정렬 시퀀스입니다. 지원 되는 데이터 정렬 시퀀스의 목록을 참조 하세요 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)합니다.|  
|Description||  
|전용|"Yes" 또는 "No"|  
|SourceDB|정규화 된 경로 포함 하는 디렉터리 0 개 이상의 [테이블 무료](../../odbc/microsoft/visual-foxpro-terminology.md), 또는 절대 경로 및 파일 이름에 대 한를 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.|  
|SourceType|"Dbc 입니다" 또는 "DBF"|  
|버전||  
  
 드라이버 관리자는 사용자 정보에 게 데이터 원본 이름을 지정 하지 않으면 (설정에 따라 합니다 *fDriverCompletion* 인수) 하 고 계속 합니다. 자세한 정보가 필요한 경우 Visual FoxPro ODBC 드라이버는 메시지 대화 상자를 표시 합니다.  
  
 자세한 내용은 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 에 *ODBC 프로그래머 참조*합니다.
