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
ms.openlocfilehash: 788f0b8c69636ad9bf93de73632abc911a0fb0e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898762"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 **SQLGetTypeInfo** 에서 생성 된 테이블에 반환 되는 형식 (TYPE_NAME)의 이름은 데이터 원본에서 가장 일반적으로 사용 되는 이름입니다.  
  
 바이트, 카운터, Double, Single, Long 및 Short 데이터 형식에 대 한 검색 가능 열에 SQL_ALL_EXCEPT_LIKE 반환 됩니다. ODBC 정식 변환 함수를 사용 하 여 값을 문자로 변환한 다음 비교를 수행 하 여 이와 같은 기능을 수행할 수 있습니다.
