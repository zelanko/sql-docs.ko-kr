---
title: 드라이버 아키텍처 개요 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd55290e09fbd35f5a1559ce4209693ef8eaaf73
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303464"
---
# <a name="driver-architecture-overview"></a>드라이버 아키텍처 개요
Microsoft Visual FoxPro ODBC 드라이버는 개방형 데이터베이스 연결(ODBC) 인터페이스를 통해 Microsoft Visual FoxPro 데이터베이스 또는 FoxPro 테이블을 열고 쿼리할 수 있는 32비트 드라이버입니다. 다음과 같은 유형의 응용 프로그램을 사용하여 FoxPro 데이터에 액세스할 수 있습니다.  
  
-   마이크로소프트 엑셀 또는 마이크로소프트 워드와 같은 마이크로소프트 오피스 응용 프로그램, ODBC와 통신 하는 마이크로소프트 쿼리를 사용 하 여.  
  
-   ODBC SDK API를 사용하는 Microsoft 시각적 C++ 또는 C로 작성된 응용 프로그램입니다.  
  
-   응용 프로그램에 대한 마이크로 소프트 비주얼 베이직 또는 마이크로 소프트 비주얼 기본으로 작성된 응용 프로그램입니다.  
  
 각각의 경우 정보 요청은 ODBC API를 사용합니다. ODBC 드라이버 관리자는 Visual FoxPro ODBC 드라이버와 협력하여 FoxPro 테이블 및 데이터베이스에서 데이터를 열고 검색합니다.  
  
 아키텍처는 다음 다이어그램에 표시됩니다.  
  
 ![ODBC 드라이버 아키텍처 표시](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Visual FoxPro 용어](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [비주얼 폭스프로 ODBC 드라이버 설치 및 구성](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Visual FoxPro ODBC 드라이버 사용](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
