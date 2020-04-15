---
title: SQLParam옵션 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd714ce7774265a2afd00d42894d644a516bc402
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299473"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 응용 프로그램이 [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)에 의해 할당 된 매개 변수 집합에 대 한 여러 값을 지정할 수 있습니다. 매개 변수 집합에 대해 여러 값을 지정하는 기능은 대량 삽입 및 데이터 원본이 다양한 매개 변수 값으로 동일한 SQL 문을 여러 번 처리해야 하는 기타 작업에 유용합니다. 예를 들어 응용 프로그램은 **INSERT** 문과 연결된 매개 변수 집합에 대해 세 가지 값 집합을 지정한 다음 **INSERT** 문을 한 번 실행하여 세 개의 삽입 작업을 수행할 수 있습니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLParamOptions를](../../odbc/reference/syntax/sqlparamoptions-function.md) 참조하십시오.
