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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b243e8ae2dc931830a249d4392da308e68722cdf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300053"
---
# <a name="the-odbc-cursor-library"></a>ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 블록 및 스크롤 가능 커서는 많은 응용 프로그램에 매우 유용한 추가 기능입니다. 그러나 모든 드라이버가 블록과 스크롤 가능 커서를 지 원하는 것은 아닙니다. 데이터 업데이트에서 설명 하는 위치 지정 update 및 delete 문과 **SQLSetPos**의 경우에도 마찬가지입니다. 따라서 이전에는 MDAC (Microsoft Data Access Components) SDK에 포함 된 Windows SDK의 ODBC 구성 요소가 커서 라이브러리를 포함 합니다. 커서 라이브러리는 Open Group Standard CLI 규칙 수준을 충족 하는 모든 드라이버에 대 한 블록, 정적 커서, 위치 지정 update 및 delete 문과 **SQLSetPos** 를 구현 합니다. ODBC 응용 프로그램을 사용 하 여 커서 라이브러리를 재배포할 수 있습니다. 자세한 내용은 SDK의 사용권 계약을 참조 하세요.  
  
 커서 라이브러리를 사용 하기 위해 응용 프로그램은 데이터 원본에 연결 하기 전에 SQL_ATTR_ODBC_CURSORS 연결 특성을 설정 합니다. 커서 라이브러리에 대 한 자세한 내용은 [부록 F: ODBC 커서 라이브러리](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)를 참조 하십시오.
