---
title: 드라이버 및 데이터 소스 정보 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307224"
---
# <a name="about-drivers-and-data-sources"></a>드라이버 및 데이터 원본 정보
*드라이버는* ODBC 요청을 처리하고 데이터를 응용 프로그램에 반환하는 구성 요소입니다. 필요한 경우 드라이버는 응용 프로그램의 요청을 데이터 원본에서 이해하는 형식으로 수정합니다. 컴퓨터에서 드라이버를 추가하거나 삭제하려면 드라이버의 설치 프로그램을 사용해야 합니다.  
  
 *데이터 원본은* 드라이버가 액세스하는 데이터베이스 또는 파일이며 데이터 원본 이름(DSN)으로 식별됩니다. ODBC 데이터 원본 관리자를 사용하여 시스템에서 데이터 원본을 추가, 구성 및 삭제합니다. 사용할 수 있는 데이터 원본의 형식은 다음 표에 설명되어 있습니다.  
  
|데이터 원본|설명|  
|-----------------|-----------------|  
|사용자|사용자 DSN은 컴퓨터에 로컬이며 현재 사용자만 사용할 수 있습니다. HKEY_CURRENT_USER 레지스트리 하위 트리에 등록됩니다.|  
|시스템|시스템 DSN은 사용자 전용이 아니라 컴퓨터에 로컬입니다. 시스템 또는 권한이 있는 사용자는 시스템 DSN으로 설정된 데이터 원본을 사용할 수 있습니다. 시스템 DSN은 HKEY_LOCAL_MACHINE 레지스트리 하위 트리에 등록됩니다.|  
|파일|파일 DSN은 동일한 드라이버가 설치되어 데이터베이스에 액세스할 수 있는 모든 사용자 간에 공유할 수 있는 파일 기반 소스입니다. 이러한 데이터 원본은 사용자 전용일 필요도 아니거나 컴퓨터에 로컬이어야 합니다. 파일 데이터 원본 이름은 전용 레지스트리 항목으로 식별되지 않습니다. 대신 .dsn 확장명을 가진 파일 이름으로 식별됩니다.|  
  
 사용자 및 시스템 데이터 원본은 컴퓨터에 로컬이기 때문에 컴퓨터 *데이터* 원본이라고 합니다.  
  
 이러한 각 데이터 원본에는 **ODBC 데이터 원본 관리자** 대화 상자에 탭이 있습니다. 사용 가능한 데이터 소스에 대한 자세한 내용은 [데이터 소스](../../odbc/reference/data-sources.md)를 참조하세요.
