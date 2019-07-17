---
title: ODBC 커서 라이브러리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a896a5bb41c5530c65573fa22c418199a043f8fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114066"
---
# <a name="the-odbc-cursor-library"></a>ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 블록 및 스크롤 가능 커서는 대부분의 응용 프로그램에 대 한 매우 유용한 추가 합니다. 그러나 일부 드라이버 블록 및 스크롤 가능 커서를 지원합니다. 현재 위치 업데이트 및 delete 문을 동일 및 **SQLSetPos**, 데이터 업데이트에서 설명 하는 합니다. 따라서 이전에 Microsoft 데이터 액세스 구성 요소 (MDAC) SDK에 포함 된 Windows SDK의 ODBC 구성 요소에는 커서 라이브러리가 포함 됩니다. 블록, 정적 커서, 위치 지정된 update 및 delete 문은 커서 라이브러리를 구현 하 고 **SQLSetPos** 열기 그룹 표준 CLI 규칙 수준을 충족 하는 모든 드라이버에 대 한 합니다. ODBC 응용 프로그램을 사용 하 여 커서 라이브러리를 재배포할 수 있습니다. 자세한 내용은 SDK에서 사용권 계약을 참조 하세요.  
  
 커서 라이브러리를 사용 하려면 응용 프로그램 데이터 원본에 연결 하기 전에 SQL_ATTR_ODBC_CURSORS 연결 특성을 설정 합니다. 커서 라이브러리에 대 한 자세한 내용은 참조 하세요. [부록 f: ODBC 커서 라이브러리](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)합니다.
