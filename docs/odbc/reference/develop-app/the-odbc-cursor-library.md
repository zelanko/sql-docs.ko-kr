---
title: ODBC 커서 라이브러리 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300053"
---
# <a name="the-odbc-cursor-library"></a>ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 블록 및 스크롤 가능한 커서는 많은 응용 프로그램에 매우 유용합니다. 그러나 모든 드라이버가 블록 및 스크롤 가능한 커서를 지원하는 것은 아닙니다. 데이터 업데이트에서 설명하는 위치 업데이트 및 삭제 문 및 **SQLSetPos도**마찬가지입니다. 따라서 이전에 Microsoft 데이터 액세스 구성 요소(MDAC) SDK에 포함 된 Windows SDK의 ODBC 구성 요소에는 커서 라이브러리가 포함됩니다. 커서 라이브러리는 오픈 그룹 표준 CLI 준수 수준을 충족하는 모든 드라이버에 대해 블록, 정적 커서, 위치 업데이트 및 삭제 문을 구현하고 **SQLSetPos를** 구현합니다. 커서 라이브러리는 ODBC 응용 프로그램과 함께 재배포될 수 있습니다. 자세한 내용은 SDK의 라이선스 계약을 참조하십시오.  
  
 커서 라이브러리를 사용 하려면 응용 프로그램은 데이터 원본에 연결 하기 전에 SQL_ATTR_ODBC_CURSORS 연결 특성을 설정 합니다. 커서 라이브러리에 대한 자세한 내용은 [부록 F: ODBC 커서 라이브러리를](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)참조하십시오.
