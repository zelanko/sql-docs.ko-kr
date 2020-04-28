---
title: 보고서 서버 데이터베이스가 구성 되지 않음 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bb5dd5968930319532a29ff7c3909c36af99b3a0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952116"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>보고서 서버 데이터베이스가 올바르게 구성되지 않음(업그레이드 관리자)
  보고서 서버 구성이 완료되지 않아 업그레이드가 차단되었습니다. 보고서 서버 데이터베이스가 구성되어 있지 않습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 설치 프로그램은 완전하게 구성된 보고서 서버 인스턴스만 업그레이드할 수 있습니다. 계속하려면 보고서 서버 데이터베이스를 구성하거나 Microsoft Windows **제어판** 을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에서 보고서 서버 기능을 제거합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 제거한 후에는 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 업그레이드할 수 있습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 보고서 서버 데이터베이스를 구성하지 않은 경우 보고서 서버가 작동하지 않으므로 업그레이드하기 전에 보고서 서버를 제거해야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 제거에 대한 자세한 내용은 [Reporting Services 2012 제거](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\))를 참조하십시오. 이 항목에서는 특정 버전을 제거하는 방법에 대해 설명하며, 절차는 이전 버전과 비슷합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 관리자를 &#40;업그레이드 문제를 Reporting Services&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
