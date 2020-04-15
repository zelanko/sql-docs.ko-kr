---
title: SQLDriverConnect (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307094"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 또는 [사용 중인 테이블의](../../odbc/microsoft/visual-foxpro-terminology.md)디렉토리일 수 있는 기존 데이터 원본에 연결합니다. ODBC 속성 키워드 UID 및 PWD는 무시됩니다. 다음 표에는 지원되는 추가 특성 키워드가 나열되어 있습니다.  
  
|ODBC 속성 키워드|특성 값|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC 드라이버에서 무시되지만 오류를 생성하지는 않습니다.|  
|PWD|Visual FoxPro ODBC 드라이버에서 무시되지만 오류를 생성하지는 않습니다.|  
|드라이버|비주얼 폭스프로 ODBC 드라이버의 이름과 위치; 드라이버 관리자에 의해 구현됩니다.|  
  
|비주얼 폭스프로 ODBC 드라이버 속성 키워드|특성 값|  
|-------------------------------------------------|---------------------|  
|백그라운드 페치|"예" 또는 "아니오"|  
|한 부씩 인쇄|"기계" 또는 기타 정렬 순서. 지원되는 정렬 시퀀스 목록은 [COLLATE SET을](../../odbc/microsoft/set-collate-command.md)참조하십시오.|  
|설명||  
|단독|"예" 또는 "아니오"|  
|SourceDB|0개 이상의 [자유 테이블을](../../odbc/microsoft/visual-foxpro-terminology.md)포함하는 디렉터리또는 [데이터베이스의](../../odbc/microsoft/visual-foxpro-terminology.md)절대 경로 및 파일 이름을 포함하는 완전 한 경로입니다.|  
|SourceType|"DBC" 또는 "DBF"|  
|버전||  
  
 데이터 원본 이름을 지정하지 않으면 드라이버 관리자는 사용자에게 정보를 묻는 메시지를 *표시합니다(fDriverCompletion* 인수설정에 따라 다름). 추가 정보가 필요한 경우 Visual FoxPro ODBC 드라이버에 프롬프트 대화 상자가 표시됩니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 를 참조하십시오.
