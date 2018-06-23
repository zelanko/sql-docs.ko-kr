---
title: 호환 되지 않는 데이터베이스 엔진 서버 데이터 정렬 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 5a81084ff6eba37d8a6fcc2643a760d879dcf13c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092320"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>호환되지 않는 데이터베이스 엔진 서버 데이터 정렬(업그레이드 관리자)
  업그레이드 관리자 검색 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 인스턴스를 사용 하 여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 는 호환 되지 않는 서버 데이터 정렬을 사용 하도록 구성 된 합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드입니다.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 관리자 검색 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 인스턴스를 사용 하 여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 는 호환 되지 않는 서버 데이터 정렬을 사용 하도록 구성 된 합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드는 SharePoint 공유 서비스 아키텍처를 사용 합니다. SharePoint는 대/소문자를 구분하도록 구성된 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 또는 서버 데이터 정렬 또는 이진 서버 데이터 정렬을 지원하지 않습니다. 호환되지 않는 데이터 정렬에는 기본적으로 대/소문자 구분되는 데이터 정렬 또는 기본적으로 호환되지만 다음 데이터 정렬 지정자 중 하나로 구성된 이진 및 기본 데이터 정렬을 포함합니다.  
  
-   **이진**  
  
-   **대/소문자 구분**  
  
-   **이진 코드 포인트**  
  
 현재 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서버 데이터 정렬은 호환되지 않으므로 업그레이드가 차단됩니다.  
  
## <a name="corrective-action"></a>수정 동작  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서버 데이터 정렬 속성은 변경할 수 없습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 업그레이드를 완료할 수 없습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 호환되는 서버 데이터 정렬을 사용 중인 새 서버로 마이그레이션해야 합니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [Reporting Services 업그레이드 및 마이그레이션](http://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [SQL Server 데이터 정렬 선택](http://go.microsoft.com/fwlink/?LinkId=233226)  
  
  