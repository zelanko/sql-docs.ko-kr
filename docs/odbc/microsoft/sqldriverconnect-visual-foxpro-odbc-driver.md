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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e270f8c9be42dc109adeaa49acb84f29f2b9511
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307094"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 기존 데이터 원본에 연결 합니다 .이 데이터 원본에는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 또는 [빈 테이블](../../odbc/microsoft/visual-foxpro-terminology.md)의 디렉터리를 사용할 수 있습니다. ODBC 특성 키워드인 UID 및 PWD는 무시 됩니다. 다음 표에서는 지원 되는 추가 특성 키워드를 보여 줍니다.  
  
|ODBC attribute 키워드|특성 값|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC 드라이버에서 무시 되지만 오류를 생성 하지는 않습니다.|  
|PWD|Visual FoxPro ODBC 드라이버에서 무시 되지만 오류를 생성 하지는 않습니다.|  
|드라이버|Visual FoxPro ODBC 드라이버의 이름 및 위치입니다. 드라이버 관리자에 의해 구현 됩니다.|  
  
|Visual FoxPro ODBC 드라이버 특성 키워드|특성 값|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Yes" 또는 "No"|  
|한 부씩 인쇄|"Machine" 또는 기타 데이터 정렬 순서입니다. 지원 되는 데이터 정렬 순서 목록은 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)을 참조 하세요.|  
|설명||  
|단독|"Yes" 또는 "No"|  
|SourceDB|0 개 이상의 [사용 가능한 테이블이](../../odbc/microsoft/visual-foxpro-terminology.md)포함 된 디렉터리의 정규화 된 경로 또는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)의 절대 경로 및 파일 이름입니다.|  
|SourceType|"DBC" 또는 "DBF"|  
|버전||  
  
 데이터 원본 이름을 지정 하지 않으면 드라이버 관리자는 사용자에 게 정보를 묻는 메시지를 표시 한 후 ( *Fdrivercompletion* 인수의 설정에 따라) 계속 합니다. 추가 정보가 필요한 경우 Visual FoxPro ODBC 드라이버는 프롬프트 대화 상자를 표시 합니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 를 참조 하세요.
