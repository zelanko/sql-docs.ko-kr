---
title: 오류 로그 모니터링
description: SQL Server 오류 로그, Windows 애플리케이션 로그 및 SQL Server Management Studio 로그 파일 뷰어를 사용하여 SQL Server와 관련된 문제를 해결합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server]
- database performance [SQL Server], errors
- Windows application logs [SQL Server]
- monitoring performance [SQL Server], errors
- server performance [SQL Server], errors
- comparing error and application log output
- errors [SQL Server], logs
- tuning databases [SQL Server], errors
- database monitoring [SQL Server], errors
- SQL Server error log
- logs [SQL Server], SQL Server error logs
- error logs [SQL Server]
- logs [SQL Server], Windows application logs
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9acc379c39cbaafc71ed4117fe3760d6ae269eb4
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900197"
---
# <a name="monitoring-the-error-logs"></a>오류 로그 모니터링
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 특정 시스템 이벤트와 사용자 정의 이벤트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 애플리케이션 로그에 기록합니다. 두 가지 로그 모두 모든 기록된 이벤트에 자동으로 타임스탬프를 남깁니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 있는 정보를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 문제를 해결할 수 있습니다.  
  
 Windows 애플리케이션 로그에서 Windows 운영 체제 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 발생하는 이벤트의 전체적인 모습을 볼 수 있습니다. Windows 이벤트 뷰어를 사용하여 Windows 애플리케이션 로그를 보고 정보를 필터링할 수 있습니다. 예를 들어 정보, 경고, 오류, 성공 감사 및 실패 감사와 같은 이벤트들을 필터링할 수 있습니다.  
  
## <a name="comparing-error-and-application-log-output"></a>오류 및 애플리케이션 로그 출력 비교  
 문제의 원인을 확인하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 Windows 애플리케이션 로그를 모두 사용할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 모니터링할 때 원인을 알 수 없는 오류 메시지가 표시될 수 있습니다. 이 경우 두 로그 간의 이벤트에 대한 날짜와 시간을 비교하면 가능한 원인 목록을 좁혀 갈 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 로그 파일 뷰어를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 및 Windows 로그를 단일 목록으로 통합할 수 있어 관련된 서버 이벤트와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트를 쉽게 이해할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서의 "로그 파일 뷰어" 항목을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[SQL Server 오류 로그 보기](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 이 로그를 보는 방법에 대해 설명합니다.|  
|[Windows 애플리케이션 로그 보기](../../tools/configuration-manager/viewing-the-windows-application-log.md)|Windows 애플리케이션 로그 및 이 로그를 보는 방법에 대해 설명합니다.|  
  
  
