---
title: '사례 연구: Microsoft Dynamics ERP와 SQL Server 2014 Replication for Scalability and Performance를 사용 하 여 엔터프라이즈 에코 시스템 구축 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 2b0b5ab7-4e08-431a-bd59-360177c4565c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64a1423295b8117640de555a7132a44af98b87c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470104"
---
# <a name="case-study-building-an-enterprise-ecosystem-with-microsoft-dynamics-erp-and-sql-server-2014-replication-for-scalability-and-performance"></a>사례 연구: 확장성과 성능을 위해 Microsoft Dynamics ERP와 SQL Server 2014 Replication을 사용하여 엔터프라이즈 에코시스템 빌드

  **요약:** 이 문서에서는 다음 시나리오를 다룹니다.  
SQL Server 2014의 트랜잭션 복제를 사용 하 여 Dynamics AX 클라이언트의 트랜잭션을 여러 노드에 분산 하는 방법. 데이터가 전체 노드에서 실시간으로 유지 관리되므로 트랜잭션 복제에서 데이터 중복성을 제공하여 데이터 가용성을 늘리고 더 효율적인 성능 분석에 사용할 수 있는 데이터를 포함합니다.  
Microsoft Dynamics ERP에서 트래잭션 복제를 활용하여 확장성이 뛰어난 엔터프라이즈 에코시스템을 구축할 때 관련된 세부 사항을 이해하는 방법. AX의 기본 기능을 사용자 지정하지 않고도 고성능과 확장성을 제공합니다.  
  
 일반적으로 트랜잭션 복제는 높은 처리량이 필요한 서버 간 워크플로에 사용됩니다. 이러한 시나리오의 예로 확장성 및 가용성 향상, 데이터 웨어하우징 및 보고, 여러 사이트의 데이터 통합, 다른 유형의 데이터 통합, 일괄 처리 작업 오프로드 등을 들 수 있습니다. 이 백서에서는 Microsoft Dynamics ERP에서 트랜잭션 복제를 활용하는 고유한 시나리오 및 관련 패턴을 설명합니다. 또한 ERP(엔터프라이즈 리소스 계획) 관련 엔터프라이즈 솔루션을 구축하기 위해 트랜잭션 복제를 고려할 경우의 문제와 모범 사례 및 각 단계의 성능 분석에 대해서도 다룹니다.  
  
 이 콘텐츠는 개발자, 설계자 및 데이터베이스 관리자에게 적합합니다. 여기서는 이 백서의 독자가 SQL Server 관리 환경뿐만 아니라 SQL Server 2008, 2012 또는 2014에 대한 기본 지식이 있다고 가정합니다.  
  
 **기록기:** Prabhakaran Sethuraman (PRAB), Microsoft  
  
 **기술 검토자:** Prabhakaran Sethuraman (PRAB), Microsoft; Santosh Padhy, Microsoft; Pavel Majstrov, Microsoft; Karthik Sankaranarayanan, Microsoft; Jon Acone, Microsoft; David Stahlkopf, Microsoft; Kent Oldenburger, Microsoft; Microsoft; Mandi Ohlinger, Jason Roth, Microsoft  
  
 **게시 날짜:** 2015년 10월  
  
 **적용 대상:** SQL Server 2008, SQL Server 2012 및 SQL Server 2014  
  
 문서를 검토 하려면 다운로드 하시기를  
        [사례 연구: 확장성 및 성능에 대 한 Microsoft Dynamics ERP와 SQL Server 2014 복제를 사용 하 여 엔터프라이즈 에코 시스템 구축](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/A%20Case%20Study%20Using%20Replication%20to%20Build%20an%20Enterprise%20Ecosystem%20in%20Microsoft%20Dynamics%20ERP%20for%20Scalability%20and%20Performance.docx) Word 문서입니다.  
  
  
