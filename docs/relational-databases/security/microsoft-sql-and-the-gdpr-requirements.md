---
title: "Microsoft SQL 및 GDPR 요구 사항 | Microsoft Docs"
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql
ms.reviewer: 
ms.suite: 
ms.technology: sql-security
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 2
author: barbkess
ms.author: ronitr
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: d533818e9498237316dabc08fc538caa2ac31c63
ms.openlocfilehash: f236ff85204ba08e8c02d5e680a4de43f021b9aa
ms.contentlocale: ko-kr
ms.lasthandoff: 06/07/2017

---
# <a name="guide-to-enhancing-privacy-and-addressing-gdpr-requirements-with-the-microsoft-sql-platform"></a>Microsoft SQL 플랫폼 요구 사항이 향상 시켜 개인 정보 및 주소 지정 GDPR를 가이드


## <a name="summary"></a>요약
2018, 년 5 월 25에 개인 정보 유럽 규칙에 따라 보호 권리, 보안 및 규정 준수에 대 한 새 전역 모음을 설정 하는 영향 때문입니다. 일반 데이터 보호 규정 또는 GDPR은 근본적으로 정보 보호 하 고 개인의 개인 정보 보호를 사용 하도록 설정 하며 strict 전역 개인 정보 보호 요구 사항이 어떻게 개인 데이터와 관련 된 관리 되 고 개별 선택 항목을 유지 하는 동안 보호 설정 

Microsoft SQL 고객에 게 영향을 받습니다 GDPR, 관리 클라우드 기반 온-프레미스 데이터베이스 또는 둘 다 자신의 데이터베이스 시스템에서 데이터 조건에 맞는 적절 하 게 처리 하 고 GDPR 원칙에 따라 보호 해야 합니다. 즉 많은 고객은 검토 하거나 해당 데이터베이스 관리 및 데이터 처리 프로시저를 수정 하려면 특히 데이터 처리는 GDPR에 규정 된 대로 보안에 중점을 두기 합니다.

Microsoft SQL 기반 기술 보호 및 데이터베이스 수준에서와 같거나 이보다 뒤에 데이터의 관리 효율성을 개선 하 고 데이터에 위험을 줄이는 데 사용할 수 있는 다양 한 기본 제공 보안 기능을 제공 합니다. 이 문서를 이러한 기능을 검사 하 고는 GDPR의 데이터 개인 정보 보호 목표를 실현을 위한 Microsoft SQL을 사용 하 여 Microsoft의 접근 방식 중 일부를 공유 합니다.
   
  
**기록기:** Ronit Reger

**기술 검토자:** Conor Cunningham; Joachim 해머; Shai Kariv; Julie Koesmarno; Alice Kupcik; Ron Matchoro; Gilad Mittelman; Dan Rediske; Tomer Weisberg 
  
**게시 날짜:** 2017 년 5 월  
  
**적용 대상:** SQL Server (모든 버전), Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스, 분석 플랫폼 시스템 
  
문서를 검토 하려면 다운로드 하십시오는 [개인 정보 보호를 향상 및 Microsoft SQL 플랫폼 GDPR 요구 사항을 해결 가이드](http://download.microsoft.com/download/4/9/4/4948194B-A613-49ED-90A5-5144313549AB/microsoft-sql-and-the-gdpr.pdf) 문서.   

