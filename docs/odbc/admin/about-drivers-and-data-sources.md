---
title: 드라이버 및 데이터 원본에 대 한 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6422e855b126245fd7118ce2518538aa0305484a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="about-drivers-and-data-sources"></a>드라이버 및 데이터 원본에 대 한
*드라이버* ODBC 요청을 처리 하 고 응용 프로그램에 데이터를 반환 하는 구성 요소입니다. 필요한 경우 드라이버는 데이터 원본에서 인식 하는 형식으로 응용 프로그램의 요청을 수정 합니다. 드라이버의 설치 프로그램을 사용 하 여를 추가 하 여 드라이버를 컴퓨터에서 삭제 해야 합니다.  
  
 *데이터 원본* 는 데이터베이스 또는 드라이버에서 액세스 하는 파일 및 데이터 원본 이름 (DSN)으로 식별 됩니다. ODBC 데이터 원본 관리자를 사용 하 여 추가, 구성 및 데이터 원본 시스템에서 삭제 합니다. 사용할 수 있는 데이터 원본 유형에 다음 표에 설명 되어 있습니다.  
  
|데이터 원본|Description|  
|-----------------|-----------------|  
|사용자|사용자 Dsn는 컴퓨터에 로컬 이며 현재 사용자만 사용할 수 있습니다. 이러한 항목은 HKEY_CURRENT_USER 레지스트리 하위 트리에 등록 됩니다.|  
|시스템|시스템 Dsn은 사용자에 게 전용 하지 않고 컴퓨터에 로컬입니다. 시스템 또는 권한이 있는 사용자 시스템 DSN 사용 하 여 설정 데이터 원본을 사용할 수 있습니다. 시스템 Dsn 레지스트리 하위 트리 HKEY_LOCAL_MACHINE에에서 등록 됩니다.|  
|파일|파일 Dsn는 동일한 드라이버가 설치 되어 있는 모든 사용자가 공유할 수 있으며이 고 따라서 데이터베이스에 액세스할 수 있는 파일 기반 소스입니다. 이러한 데이터 원본은 사용자에 전용 될 필요 없으며 한 컴퓨터. 파일 데이터 원본 이름 전용된 레지스트리 항목;으로 식별 되지 않습니다. 대신,.dsn 확장명이 파일 이름으로 식별 됩니다.|  
  
 사용자 및 시스템 데이터 원본 이라고 통칭 *컴퓨터* 로컬 컴퓨터에 있기 때문에 데이터 원본입니다.  
  
 이러한 각 데이터 원본에는 탭는 **ODBC 데이터 원본 관리자** 대화 상자. 사용 가능한 데이터 소스에 대한 자세한 내용은 [데이터 소스](../../odbc/reference/data-sources.md)를 참조하세요.
