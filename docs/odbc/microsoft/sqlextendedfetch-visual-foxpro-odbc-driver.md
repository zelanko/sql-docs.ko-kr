---
title: SQLExtendedFetch (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298653"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 수준 2  
  
 [SQLFetch와](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) 유사하지만 각 열에 대한 배열을 사용하여 여러 행을 반환합니다. 결과 집합은 앞으로 스크롤할 수 있으며 커서가 정적이고 앞으로만 지정되지 않은 경우 뒤로 스크롤할 수 있습니다.  
  
 기본적으로 Visual FoxPro ODBC 드라이버는 FoxPro 테이블에서 삭제된 것으로 표시된 행을 반환하지 않습니다. 삭제로 표시되었지만 테이블에서 아직 제거되지 않은 행은 결과 집합 커서에 포함되지 않습니다. [삭제 된 SET](../../odbc/microsoft/set-deleted-command.md) 명령을 사용 하 여이 동작을 변경할 수 있습니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLExtendedFetch를](../../odbc/reference/syntax/sqlextendedfetch-function.md) 참조하십시오.
