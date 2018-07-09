---
title: 항목 수준 작업 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- item-level tasks [Reporting Services]
ms.assetid: fdeb7bc3-167a-4342-84e3-32e3faa1fa39
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 43da85b3e7435bb3685090ae1f2e80830793b3f8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150144"
---
# <a name="item-level-tasks"></a>항목 수준의 태스크
  항목 수준 태스크는 보고서, 폴더, 보고서 모델, 리소스 또는 공유 데이터 원본과 관련된 사용 권한 모음입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 보고서 서버 사이트에 전체적으로 적용되는 시스템 수준 태스크도 있습니다. 자세한 내용은 [시스템 수준 태스크](tasks-and-permissions-system-level-tasks.md)를 참조하세요. 일반적인 사용 권한과 작업에 대 한 자세한 내용은 참조 하세요. [Tasks and Permissions](tasks-and-permissions.md)합니다.  
  
> [!NOTE]  
>  이러한 태스크를 프로그래밍 방식으로 수행하는 경우에는 항목 수준 작업을 지원하는 메서드를 사용해야 합니다. 자세한 내용은 <xref:ReportService2010.ReportingService2010.ListTasks%2A> 및 <xref:ReportService2010.ReportingService2010.ListRoles%2A>를 참조하세요.  
  
## <a name="permissions-in-item-level-tasks"></a>항목 수준 태스크의 사용 권한  
 다음 표에서는 항목 수준 태스크, 각 태스크에 포함되어 있는 사용 권한 및 해당 사용 권한이 적용되는 항목을 나열합니다. 나열된 사용 권한은 각 태스크를 통해 사용할 수 있는 기능을 보다 정확하게 설명하기 위한 참고용입니다.  
  
 공유 데이터 집합은 보고서와 동일한 사용 권한 집합을 사용하고, 보고서 파트는 리소스와 동일한 사용 권한 집합을 사용합니다.  
  
|태스크|적용 항목|사용 권한|  
|----------|---------------------|-----------------|  
|보고서 사용|보고서|내용 읽기<br /><br /> 보고서 정의 읽기<br /><br /> 속성 읽기|  
|보고서 사용|공유 데이터 집합|내용 읽기<br /><br /> 보고서 정의 읽기<br /><br /> 속성 읽기|  
|링크된 보고서 만들기|보고서|링크 만들기<br /><br /> 속성 읽기|  
|모든 구독 관리|보고서|속성 읽기<br /><br /> 모든 구독 읽기<br /><br /> 모든 구독 만들기<br /><br /> 모든 구독 삭제<br /><br /> 모든 구독 업데이트|  
|데이터 원본 관리|폴더|데이터 원본 만들기|  
|데이터 원본 관리|솔루션 탐색기|속성 업데이트<br /><br /> 업데이트 내용 삭제<br /><br /> 속성 읽기|  
|폴더 관리|폴더|폴더 만들기<br /><br /> 업데이트 속성 삭제<br /><br /> 속성 읽기|  
|개별 구독 관리|보고서|속성 읽기<br /><br /> 구독 만들기<br /><br /> 구독 삭제<br /><br /> 구독 읽기<br /><br /> 구독 업데이트|  
|모델 관리|폴더|모델 만들기|  
|모델 관리|모델|속성 읽기<br /><br /> 내용 읽기<br /><br /> 업데이트 내용 삭제<br /><br /> 데이터 원본 읽기<br /><br /> 데이터 원본 업데이트<br /><br /> 모델 항목 권한 부여 정책 읽기<br /><br /> 모델 항목 권한 부여 정책 업데이트<br /><br /> 업데이트 속성 삭제|  
|보고서 기록 관리|보고서|속성 읽기<br /><br /> 보고서 기록 만들기<br /><br /> 보고서 기록 삭제<br /><br /> 읽기 정책 실행<br /><br /> 정책 업데이트<br /><br /> 보고서 기록 나열|  
|보고서 관리|폴더|보고서 만들기<br /><br /> 공유 데이터 집합 만들기에도 적용됨|  
|보고서 관리|보고서|속성 읽기<br /><br /> 업데이트 속성 삭제<br /><br /> 매개 변수 업데이트<br /><br /> 데이터 원본 읽기<br /><br /> 데이터 원본 업데이트<br /><br /> 보고서 정의 읽기<br /><br /> 보고서 정의 업데이트<br /><br /> 읽기 정책 실행<br /><br /> 정책 업데이트|  
|보고서 관리|공유 데이터 집합|속성 읽기<br /><br /> 업데이트 속성 삭제<br /><br /> 매개 변수 업데이트<br /><br /> 데이터 원본 읽기<br /><br /> 데이터 원본 업데이트<br /><br /> 보고서 정의 읽기<br /><br /> 보고서 정의 업데이트<br /><br /> 읽기 정책 실행<br /><br /> 정책 업데이트|  
|리소스 관리|폴더|리소스 만들기|  
|리소스 관리|리소스|속성 업데이트<br /><br /> 업데이트 내용 삭제<br /><br /> 속성 읽기|  
|리소스 관리|보고서 파트|속성 업데이트<br /><br /> 업데이트 내용 삭제<br /><br /> 속성 읽기|  
|개별 항목의 보안 설정|보고서, 리소스, 데이터 원본, 공유 데이터 집합, 폴더|보안 정책 읽기 보안 정책 업데이트|  
|데이터 원본 보기|데이터 원본|내용 읽기<br /><br /> 속성 읽기|  
|폴더 보기|폴더|속성 읽기<br /><br /> 실행 및 보기<br /><br /> 보고서 기록 나열|  
|모델 보기|보고서 모델|속성 읽기<br /><br /> 내용 읽기<br /><br /> 데이터 원본 읽기|  
|보고서 보기|보고서|내용 읽기<br /><br /> 속성 읽기|  
|보고서 보기|공유 데이터 집합|내용 읽기<br /><br /> 속성 읽기|  
|리소스 보기|리소스|내용 읽기<br /><br /> 속성 읽기|  
|리소스 보기|보고서 파트|내용 읽기<br /><br /> 속성 읽기|  
  
## <a name="see-also"></a>관련 항목  
 [기본 모드 보고서 서버에 대한 사용 권한 부여](granting-permissions-on-a-native-mode-report-server.md)  
  
  
