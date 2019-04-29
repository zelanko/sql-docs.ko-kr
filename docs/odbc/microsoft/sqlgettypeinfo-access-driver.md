---
title: SQLGetTypeInfo (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a7c87c0dc81035d59e17db02a6e95c3b573523a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028696"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 (TYPE_NAME) 형식의 이름을 반환 하 여 생성 된 테이블 **SQLGetTypeInfo** 이름이 데이터 원본에서 가장 일반적으로 사용 됩니다.  
  
 SQL_ALL_EXCEPT_LIKE이 반환할 검색할 수 있는 열에 바이트에 대 한 카운터, Double, 단일 고 Long, Short 데이터 형식입니다. (다음 비교를 수행 하는 ODBC 정식 변환 함수를 사용 하 여 문자 값을 변환 하 여 LIKE 기능을 구현할 수 있습니다.)
