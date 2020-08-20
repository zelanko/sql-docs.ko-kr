---
description: 드라이버 아키텍처 개요
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d71a2c28825ee8c7d4e12e047234f3e336b339e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466445"
---
# <a name="driver-architecture-overview"></a>드라이버 아키텍처 개요
Microsoft Visual FoxPro ODBC 드라이버는 ODBC (Open Database Connectivity) 인터페이스를 통해 Microsoft Visual FoxPro 데이터베이스 또는 FoxPro 테이블을 열고 쿼리 하는 데 사용할 수 있는 32 비트 드라이버입니다. 다음과 같은 유형의 응용 프로그램을 사용 하 여 FoxPro 데이터에 액세스할 수 있습니다.  
  
-   Microsoft Excel 또는 Microsoft Word와 같이 Microsoft Query를 사용 하 여 ODBC와 통신 하는 Microsoft Office 응용 프로그램입니다.  
  
-   ODBC SDK API를 사용 하는 Microsoft Visual C++ 또는 C로 작성 된 응용 프로그램입니다.  
  
-   Microsoft Visual Basic 또는 Microsoft Visual Basic for Applications으로 작성 된 응용 프로그램입니다.  
  
 각 경우에서 정보에 대 한 요청은 ODBC API를 사용 합니다. ODBC 드라이버 관리자는 Visual FoxPro ODBC 드라이버와 함께 작동 하 여 FoxPro 테이블 및 데이터베이스에서 데이터를 열고 검색 합니다.  
  
 아키텍처는 다음 다이어그램에 표시 됩니다.  
  
 ![ODBC 드라이버 아키텍처 표시](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Visual FoxPro 용어](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Visual FoxPro ODBC 드라이버 설치 및 구성](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Visual FoxPro ODBC 드라이버 사용](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
