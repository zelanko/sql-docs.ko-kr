---
title: 드라이버 아키텍처 개요 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 833c953df3502eb7e5d5676da8df057734174619
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071917"
---
# <a name="driver-architecture-overview"></a>드라이버 아키텍처 개요
Microsoft Visual FoxPro ODBC 드라이버는 32 비트 드라이버를 열고 Microsoft Visual FoxPro 데이터베이스 또는 데이터베이스 연결 열기 (ODBC) 인터페이스를 통해 FoxPro 테이블을 쿼리할 수 있도록. FoxPro 데이터 응용 프로그램의 다음 형식을 사용 하 여 액세스할 수 있습니다.  
  
-   Microsoft Excel 또는 Microsoft Word와 같은 Microsoft Office 응용 프로그램을 사용 하 여 Microsoft 쿼리 ODBC를 사용 하 여 통신 합니다.  
  
-   Microsoft Visual 작성 된 응용 프로그램 C++ 또는 ODBC SDK API를 사용 하는 C입니다.  
  
-   Microsoft Visual Basic 또는 Microsoft Visual Basic for Applications로 작성 된 응용 프로그램.  
  
 각각의 경우 정보 요청에는 ODBC API를 사용합니다. ODBC 드라이버 관리자를 열고 FoxPro 테이블 및 데이터베이스에서 데이터를 검색할 Visual FoxPro ODBC 드라이버를 사용 하 여 작동 합니다.  
  
 아키텍처는 다음 다이어그램에 표시 됩니다.  
  
 ![ODBC 드라이버 아키텍처를 보여 줍니다](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Visual FoxPro 용어](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [설치 및 Visual FoxPro ODBC 드라이버를 구성 합니다.](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Visual FoxPro ODBC 드라이버 사용](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
