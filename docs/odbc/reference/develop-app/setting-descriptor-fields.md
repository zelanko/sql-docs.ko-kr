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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094252"
---
# <a name="setting-descriptor-fields"></a>설명자 필드 설정
설명자의 필드를 수정 하기 위해 응용 프로그램은 **SQLSetDescField**를 호출할 수 있습니다. 일부 필드는 읽기 전용 이며 설정할 수 없습니다. [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명을 참조 하십시오.  
  
 설명자 레코드 필드는 1 이상의 레코드 번호 (*개수*)로 설정 되 고 설명자 헤더 필드는 레코드 번호 0으로 설정 됩니다. 레코드 번호 0은 책갈피가 열 0에 포함 된 규칙에 따라 책갈피 필드를 설정 하는 데도 사용 됩니다. 이로 인해 책갈피 필드가 설명자 헤더 내에 포함 되는 것 처럼 보일 수 있지만이는 그렇지 않습니다. 책갈피 필드는 헤더 필드와는 다릅니다.  
  
 필드를 개별적으로 설정 하는 경우 응용 프로그램은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)에 정의 된 시퀀스를 따라야 합니다. 일부 필드를 설정 하면 드라이버가 다른 필드를 설정 합니다. 이렇게 하면 응용 프로그램에서 데이터 형식을 지정한 후에 항상 설명자를 사용할 수 있습니다. 응용 프로그램에서 SQL_DESC_TYPE 필드를 설정 하는 경우 드라이버는 유형을 지정 하는 다른 필드가 올바르고 일치 하는지 확인 합니다.  
  
 설명자 필드를 설정 하는 함수 호출이 실패 하면 실패 한 함수 호출 후 설명자 필드의 내용이 정의 되지 않습니다.
