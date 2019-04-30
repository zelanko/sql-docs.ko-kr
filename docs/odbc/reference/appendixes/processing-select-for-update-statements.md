---
title: SELECT FOR UPDATE 문 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f54d31426773f294a4a23f059c9f906d430056f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057030"
---
# <a name="processing-select-for-update-statements"></a>SELECT FOR UPDATE 문 처리
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 응용 프로그램은 실행 하 여 위치 지정된 update 문을 사용 하 여 업데이트 되는 결과 집합을 생성 하는 데 최대 상호 운용성을 위해 한 **업데이트에 대 한 선택** 문입니다. 커서 라이브러리를 요구 하지 않습니다 하지만 대부분의 데이터 원본 위치 지정된 update 문을 지원에서 필요 합니다.  
  
 커서 라이브러리에 있는 열을 무시를 **에 대 한 업데이트** 절을 **SELECT FOR UPDATE** 문과 문을 드라이버에 전달 하기 전에이 절을 제거 하는 것입니다. 커서 라이브러리에 SQL_ATTR_CONCURRENCY 문 특성을 이전 섹션에서 설명한 제한 함께 컨트롤 집합을 결과에서 열 수 있는지 여부를 업데이트할 수 있습니다.
