---
title: ODBC 커서 라이브러리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 861b4c98042dc5f7b94e831dc8ed1306ea8b3213
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915068"
---
# <a name="the-odbc-cursor-library"></a>ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 블록 및 스크롤 가능 커서는 많은 응용 프로그램에 매우 유용한 추가 됩니다. 그러나 일부 드라이버 블록 및 스크롤 가능 커서를 지원 합니다. 위치 지정된 업데이트의 경우에 동일한 및 delete 문 및 **SQLSetPos**, 데이터 업데이트에 대해서는 설명입니다. 따라서 ODBC 구성 요소에는 Microsoft 데이터 액세스 구성 요소 (MDAC) SDK를 포함 하는 Windows SDK의 커서 라이브러리가 포함 됩니다. 블록, 정적 커서, 위치 지정된 update 및 delete 문은 커서 라이브러리를 구현 하 고 **SQLSetPos** Open 그룹 표준 CLI 규칙 수준을 충족 하는 모든 드라이버에 대 한 합니다. ODBC 응용 프로그램; 함께 커서 라이브러리를 재배포할 수 있습니다. 자세한 내용은 SDK에서 사용권 계약을 참조 하십시오.  
  
 커서 라이브러리를 사용 하려면 응용 프로그램 데이터 원본에 연결 하기 전에 SQL_ATTR_ODBC_CURSORS 연결 특성을 설정 합니다. 커서 라이브러리에 대 한 자세한 내용은 참조 [부록 f: ODBC 커서 라이브러리](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)합니다.
