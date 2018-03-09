---
title: "드라이버 아키텍처 개요 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2778161fa117e164a4c49e57a5511b0682507b37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="driver-architecture-overview"></a>드라이버 아키텍처 개요
Microsoft Visual FoxPro ODBC 드라이버는를 열고 Microsoft Visual FoxPro 데이터베이스 또는 데이터베이스 연결 열기 (ODBC) 인터페이스를 통해 FoxPro 테이블을 쿼리할 수 있는 32 비트 드라이버. 다음과 같은 종류의 응용 프로그램을 사용 하 여 FoxPro 데이터에 액세스할 수 있습니다.  
  
-   ODBC와 통신할 수 Microsoft 쿼리를 사용 하 Microsoft Excel 또는 Microsoft Word와 같은 Microsoft Office 응용 프로그램입니다.  
  
-   Microsoft Visual c + + 또는 ODBC SDK API를 사용 하는 C로 작성 된 응용 프로그램.  
  
-   Microsoft Visual Basic 또는 Microsoft Visual Basic for Applications에서 작성 된 응용 프로그램입니다.  
  
 각각의 경우 정보 요청에는 ODBC API를 사용합니다. ODBC 드라이버 관리자를 열고 FoxPro 테이블 및 데이터베이스에서 데이터를 검색할 Visual FoxPro ODBC 드라이버와 함께 작동 합니다.  
  
 아키텍처는 다음 다이어그램에 표시 됩니다.  
  
 ![ODBC 드라이버 아키텍처 표시](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Visual FoxPro 용어](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [설치 하 고 Visual FoxPro ODBC 드라이버를 구성 합니다.](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Visual FoxPro ODBC 드라이버 사용](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
