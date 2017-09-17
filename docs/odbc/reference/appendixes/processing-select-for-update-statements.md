---
title: "UPDATE 문에 대 한 선택 처리 | Microsoft Docs"
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
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ada17f95371246e3b43e1e9482ab9595f85a8db1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="processing-select-for-update-statements"></a>UPDATE 문에 대 한 SELECT를 처리합니다.
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 상호 운용성을 극대화 응용 프로그램을 실행 하 여 위치 지정된 update 문을 사용 하 여 업데이트 되는 결과 집합을 생성 해야는 **업데이트에 대 한 선택** 문. 커서 라이브러리에 필요 하지 않으면이 있지만 대부분의 데이터 원본 위치 지정된 update 문을 지원에 필요 합니다.  
  
 커서 라이브러리에서 열을 무시는 **FOR UPDATE** 절은 **SELECT FOR UPDATE** 문과 문을 드라이버에 전달 하기 전에이 절을 제거 합니다. 에 커서 라이브러리를 이전 섹션에서 언급 한 제한 사항 함께 SQL_ATTR_CONCURRENCY 문 특성을 컨트롤 결과의 열 집합 여부를 업데이트할 수 있습니다.
