---
title: 드라이버 및 데이터 원본 정보 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dffeea3bea7e3fbfa66e534ecaa758fbc2064d5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307224"
---
# <a name="about-drivers-and-data-sources"></a>드라이버 및 데이터 원본 정보
*드라이버* 는 ODBC 요청을 처리 하 고 응용 프로그램에 데이터를 반환 하는 구성 요소입니다. 필요한 경우 드라이버는 데이터 원본에서 인식할 수 있는 형식으로 응용 프로그램의 요청을 수정 합니다. 드라이버의 설치 프로그램을 사용 하 여 컴퓨터에서 드라이버를 추가 하거나 삭제 해야 합니다.  
  
 *데이터 원본은* 드라이버에서 액세스 하는 데이터베이스 또는 파일이 며 DSN (데이터 원본 이름)으로 식별 됩니다. ODBC 데이터 원본 관리자를 사용 하 여 시스템에서 데이터 원본을 추가, 구성 및 삭제할 수 있습니다. 다음 표에서는 사용할 수 있는 데이터 원본 유형을 설명 합니다.  
  
|데이터 원본|Description|  
|-----------------|-----------------|  
|사용자|사용자 Dsn은 컴퓨터에 로컬인 것 이며 현재 사용자만 사용할 수 있습니다. HKEY_CURRENT_USER 레지스트리 하위 트리에 등록 됩니다.|  
|System (시스템)|시스템 Dsn은 사용자 전용이 아닌 컴퓨터에 로컬로 사용 됩니다. 시스템 또는 권한이 있는 사용자는 시스템 DSN을 사용 하 여 설정 된 데이터 원본을 사용할 수 있습니다. 시스템 Dsn은 HKEY_LOCAL_MACHINE 레지스트리 하위 트리에 등록 됩니다.|  
|파일|파일 Dsn은 동일한 드라이버를 설치 하 여 데이터베이스에 액세스할 수 있는 모든 사용자 들 간에 공유할 수 있는 파일 기반 원본입니다. 이러한 데이터 원본은 사용자 전용 이거나 컴퓨터에 대 한 로컬이 아니어야 합니다. 파일 데이터 원본 이름은 전용 레지스트리 항목으로 식별 되지 않습니다. 대신 확장명이. i n i 확장명을 가진 파일 이름으로 식별 됩니다.|  
  
 사용자 및 시스템 데이터 원본은 컴퓨터에 로컬로 사용 되므로 통칭 하 여 *컴퓨터* 데이터 원본 이라고 합니다.  
  
 이러한 각 데이터 원본에는 **ODBC 데이터 원본 관리자** 대화 상자에 탭이 있습니다. 사용 가능한 데이터 소스에 대한 자세한 내용은 [데이터 소스](../../odbc/reference/data-sources.md)를 참조하세요.
