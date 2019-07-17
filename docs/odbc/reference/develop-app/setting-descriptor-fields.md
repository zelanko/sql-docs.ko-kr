---
title: 설명자 필드 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34c4a6e3d98b6711c77fb50d7156207de148881a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094252"
---
# <a name="setting-descriptor-fields"></a>설명자 필드 설정
설명자 필드를 수정 하려면 응용 프로그램이 호출할 수 있습니다 **SQLSetDescField**합니다. 일부 필드는 읽기 전용 이며 설정할 수 없습니다. (참조를 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명 합니다.)  
  
 설명자 레코드 필드는 레코드 번호를 사용 하 여 설정 됩니다 (*RecNumber*) 1 이상 동안의 설명자 헤더 필드는 레코드 번호 0 사용 하 여 설정 합니다. 책갈피를 0 열에 포함 된는 규칙에 따라 책갈피 필드를 설정 하는 레코드 번호 0도 사용 됩니다. 책갈피 필드 설명자 헤더에 포함 되어 있지만이 비율이 높을수록 좋다고는 인상을 남았을 수 있습니다. 책갈피 필드 헤더 필드와에서 다릅니다.  
  
 응용 프로그램에 정의 된 순서 필드를 개별적으로 설정 하는 경우 따라야 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 다른 필드를 설정 하면 일부 필드를 설정 합니다. 이렇게 하면 설명자는 항상 응용 프로그램에는 데이터 형식 지정에 사용할 준비가 됩니다. SQL_DESC_TYPE 필드를 설정 하는 응용 프로그램, 드라이버 유효 하 고 일치 유형을 지정 하는 다른 필드는 확인 합니다.  
  
 설명자 필드를 설정 하는 함수 호출에 실패 하면 설명자 필드의 내용을 정의 되지 않습니다 실패 한 함수 호출 후.
