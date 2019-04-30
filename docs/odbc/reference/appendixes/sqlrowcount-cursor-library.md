---
title: SQLRowCount (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b3dcd9c348d83dad1e295e253cb37768fbb0abb
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473050"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLRowCount** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLRowCount**를 참조 하십시오 [SQLRowCount 함수](../../../odbc/reference/syntax/sqlrowcount-function.md)합니다.  
  
 응용 프로그램을 호출할 때 **SQLRowCount** 커서 라이브러리는 커서와 연관 된 문을 사용 하면 드라이버에서 가져온 데이터의 행 수를 반환 합니다.  
  
 응용 프로그램을 호출할 때 **SQLRowCount** 커서 라이브러리 위치 지정된 update 또는 delete 문을 사용 하 여 연결 된 문을 사용 하면 문에 의해 영향을 받는 행 수를 반환 합니다.  
  
 응용 프로그램을 호출할 때 **SQLRowCount** 후를 **선택** 문을 커서 라이브러리는-1을 반환 합니다.
