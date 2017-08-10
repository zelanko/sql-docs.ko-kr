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
ms.translationtype: HT
ms.sourcegitcommit: d533818e9498237316dabc08fc538caa2ac31c63
ms.openlocfilehash: f236ff85204ba08e8c02d5e680a4de43f021b9aa
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="guide-to-enhancing-privacy-and-addressing-gdpr-requirements-with-the-microsoft-sql-platform"></a>Microsoft SQL 플랫폼을 사용한 개인 정보 보호 향상 및 GDPR 요구 사항 해결 가이드


## <a name="summary"></a>요약
2018년 5월 25일에 개인 정보 보호 권한, 보안 및 준수에 대해 전 세계 제재를 새롭게 규정하는 유럽 개인 정보 보호법이 발효될 예정입니다. GDPR(General Data Protection Regulation)은 기본적으로 개인의 개인 정보 보호 권한을 보호하고 지원하기 위한 것으로 개인 데이터를 관리 및 보호하는 방법을 규정하는 동시에 개인의 선택을 존중하는 엄격한 전 세계 개인 정보 보호 요구 사항을 설정합니다. 

클라우드 기반 또는 온-프레미스 데이터베이스 중 무엇을 관리하든 GDPR의 적용을 받는 Microsoft SQL 고객은 데이터베이스에 있는 해당하는 데이터를 GDPR 원칙에 따라 적절하게 처리 및 보호해야 합니다. 따라서 많은 고객은 데이터베이스 관리 및 데이터 처리 절차를 검토하거나 수정해야 하며 특히, 데이터 처리에 대한 보안을 GDPR에 규정된 대로 유지해야 합니다.

Microsoft SQL 기반 기술에서는 데이터베이스 수준과 그 이상에서 데이터의 보호 및 관리 기능을 향상하고 데이터에 대한 위험을 줄일 수 있는 여러 보안 기능을 기본적으로 제공합니다. 이 문서에서는 이러한 기능을 검토하고 GDPR의 데이터 개인 정보 보호 목표를 실현하기 위해 Microsoft SQL을 사용한 Microsoft 자체의 접근 방식 몇 가지에 대해 설명합니다.
   
  
**작성자:** Ronit Reger

**기술 검토자:** Conor Cunningham, Joachim Hammer, Shai Kariv, Julie Koesmarno, Alice Kupcik, Ron Matchoro, Gilad Mittelman, Dan Rediske, Tomer Weisberg 
  
**게시일:** 2017년 5월  
  
**적용 대상:** SQL Server(모든 버전), Azure SQL Database, Azure SQL Data Warehouse, Analytics Platform System 
  
문서를 검토하려면 [Microsoft SQL 플랫폼을 사용한 개인 정보 보호 향상 및 GDPR 요구 사항 해결 가이드](http://download.microsoft.com/download/4/9/4/4948194B-A613-49ED-90A5-5144313549AB/microsoft-sql-and-the-gdpr.pdf) 문서를 다운로드하세요.   

