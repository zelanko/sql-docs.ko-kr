---
title: 드라이버 및 데이터 원본에 대 한 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e9b7229882b3b7f94e6b059e04c6496bde09641
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938049"
---
# <a name="about-drivers-and-data-sources"></a>드라이버 및 데이터 원본 정보
*드라이버* ODBC 요청을 처리 하 고 응용 프로그램에 데이터를 반환 되는 구성 요소입니다. 필요한 경우 드라이버는 데이터 원본에서 인식할 수 있는 폼에는 응용 프로그램의 요청을 수정 합니다. 드라이버의 설치 프로그램을 사용 하 여를 추가 하 여 컴퓨터에서 드라이버를 삭제 해야 합니다.  
  
 *데이터 원본* 데이터베이스 또는 드라이버에 의해 액세스 되는 파일 및 데이터 원본 이름 (DSN)으로 식별 됩니다. 추가, 구성 및 시스템에서 데이터 원본을 삭제 하려면 ODBC 데이터 원본 관리자를 사용 합니다. 사용할 수 있는 데이터 원본 유형에 다음 표에 설명 합니다.  
  
|데이터 원본|설명|  
|-----------------|-----------------|  
|사용자|사용자 Dsn을 컴퓨터에 로컬인 및 현재 사용자만 사용할 수 있습니다. HKEY_CURRENT_USER 레지스트리 하위 트리에 등록 됩니다.|  
|시스템|시스템 Dsn은 전용 사용자 대신 컴퓨터에 로컬입니다. 시스템 또는 사용자 권한으로 시스템 DSN 사용 하 여 설정 데이터 원본을 사용할 수 있습니다. 시스템 Dsn 레지스트리 하위 트리 HKEY_LOCAL_MACHINE에에서 등록 됩니다.|  
|파일|파일 Dsn는 동일한 드라이버를 설치 하는 모든 사용자가 공유할 수 있고 따라서 데이터베이스에 대 한 액세스를 제공 하는 파일 기반 원본입니다. 이러한 데이터 원본은 사용자 전용 필요 없으며 로컬 컴퓨터에. 파일 데이터 원본 이름은 전용된 레지스트리 항목으로 식별 되지 대신.dsn 확장명이 파일 이름으로 식별 됩니다.|  
  
 사용자 및 시스템 데이터 원본 이라고 통칭 *머신* 로컬 컴퓨터에 있기 때문에 데이터 원본입니다.  
  
 이러한 데이터 원본은 각각의 탭는 **ODBC 데이터 원본 관리자** 대화 상자. 사용 가능한 데이터 소스에 대한 자세한 내용은 [데이터 소스](../../odbc/reference/data-sources.md)를 참조하세요.
