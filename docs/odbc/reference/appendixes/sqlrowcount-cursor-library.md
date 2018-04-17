---
title: SQLRowCount (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a74130031623a1198eada5e2bd62a992867c4e3a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLRowCount** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLRowCount**, 참조 [SQLRowCount 함수](../../../odbc/reference/syntax/sqlrowcount-function.md)합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLRowCount** 커서와 관련 된 문을 사용 하 여 커서 라이브러리는 드라이버에서 가져온 데이터의 행 수를 반환 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLRowCount** 위치 지정된 update 또는 delete 문이와 관련 된 문을 사용 하 여 커서 라이브러리 문에 의해 영향을 받는 행 수를 반환 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLRowCount** 후 한 **선택** 문에서 커서 라이브러리는 – 1을 반환 합니다.
