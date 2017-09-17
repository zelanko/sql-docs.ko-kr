---
title: "SQLDriverConnect (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 363a727cd209f7ed3a5994f353f1e21922fe00ca
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 적용:  
  
 일 수 있는 기존 데이터 원본에 연결 하는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 의 디렉터리나 [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. UID 및 PWD ODBC 특성 키워드는 무시 됩니다. 다음 표에서 지원 되는 추가 특성 키워드를 나열 합니다.  
  
|ODBC 특성 키워드|특성 값|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC 드라이버에 의해 무시 되지만 오류가 발생 하지 않습니다.|  
|PWD|Visual FoxPro ODBC 드라이버에 의해 무시 되지만 오류가 발생 하지 않습니다.|  
|드라이버|이름 및 위치 Visual FoxPro ODBC driver. 드라이버 관리자에서 구현 됩니다.|  
  
|Visual FoxPro ODBC 드라이버 특성 키워드|특성 값|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Yes" 또는 "No"|  
|한 부씩 인쇄|"컴퓨터" 또는 다른 데이터 정렬 순서입니다. 목록이 지원 되는 데이터 정렬 시퀀스에 대 한 참조 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)합니다.|  
|Description||  
|단독|"Yes" 또는 "No"|  
|SourceDB|정규화 된 경로를 포함 하는 디렉터리 0 개 이상의 [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md), 또는 대 한 절대 경로 파일 이름을 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.|  
|SourceType|"Dbc 입니다" 또는 "DBF"|  
|버전||  
  
 드라이버 관리자는 정보에 대 한 사용자 요청 데이터 원본 이름을 지정 하지 않으면 (의 설정에 따라는 *fDriverCompletion* 인수) 하 고 계속 합니다. 자세한 정보가 필요한 경우 Visual FoxPro ODBC 드라이버는 메시지 대화 상자를 표시 합니다.  
  
 자세한 내용은 참조 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 에 *ODBC Programmer's Reference*합니다.
