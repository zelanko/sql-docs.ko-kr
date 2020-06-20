---
title: ObjectType 추적 이벤트 열 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Object Type column values
- events [SQL Server], Object Type column values
- event classes [SQL Server], Object Type column values
- Object Type column values [SQL Server]
ms.assetid: 42f85c50-34c9-49ca-955f-af9595e2707f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1f90661e5ebedc91505989c3d80dcec78436ce86
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85029143"
---
# <a name="objecttype-trace-event-column"></a>ObjectType 추적 이벤트 열
  Object Type 추적 이벤트 열은 다양한 추적 이벤트에 사용됩니다. 이 항목에서는 이 열에 사용할 수 있는 값과 해당 값의 정의에 대해 설명합니다.  
  
## <a name="object-type-column-values"></a>Object Type 열 값  
  
|값|정의|  
|-----------|----------------|  
|8259|CHECK 제약 조건|  
|8260|기본값(제약 조건 또는 독립 실행)|  
|8262|FOREIGN KEY 제약 조건|  
|8272|저장 프로시저|  
|8274|규칙|  
|8275|시스템 테이블|  
|8276|서버에 대한 트리거|  
|8277|사용자 정의 테이블|  
|8278|보기|  
|8280|확장 저장 프로시저|  
|16724|CLR 트리거|  
|16964|데이터베이스|  
|16975|Object|  
|17222|FullText 카탈로그|  
|17232|CLR 저장 프로시저|  
|17235|스키마|  
|17475|자격 증명|  
|17491|DDL 이벤트|  
|17741|관리 이벤트|  
|17747|보안 이벤트|  
|17749|사용자 이벤트|  
|17985|CLR 집계 함수|  
|17993|인라인 테이블 반환 SQL 함수|  
|18000|파티션 함수|  
|18002|복제 필터 프로시저|  
|18004|테이블 반환 SQL 함수|  
|18259|서버 역할|  
|18263|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 그룹|  
|19265|비대칭 키|  
|19277|마스터 키|  
|19280|기본 키|  
|19283|ObfusKey|  
|19521|비대칭 키 로그인|  
|19523|인증서 로그인|  
|19538|역할|  
|19539|SQL 로그인|  
|19543|Windows 로그인|  
|20034|원격 서비스 바인딩|  
|20036|데이터베이스에 대한 이벤트 알림|  
|20037|이벤트 알림|  
|20038|스칼라 SQL 함수|  
|20047|개체에 대한 이벤트 알림|  
|20051|동의어|  
|20307|시퀀스|  
|20549|끝점|  
|20801|캐시될 임시 쿼리|  
|20816|캐시될 준비된 쿼리|  
|20819|Service Broker 서비스 큐|  
|20821|UNIQUE 제약 조건|  
|21057|애플리케이션 역할|  
|21059|인증서|  
|21075|서버|  
|21076|Transact-SQL 트리거|  
|21313|어셈블리|  
|21318|CLR 스칼라 함수|  
|21321|인라인 스칼라 SQL 함수|  
|21328|파티션 구성표|  
|21333|사용자|  
|21571|Service Broker 서비스 계약|  
|21572|데이터베이스에 대한 트리거|  
|21574|CLR 테이블 반환 함수|  
|21577|내부 테이블(예: XML 노드 테이블, 큐 테이블)|  
|21581|Service Broker 메시지 유형|  
|21586|Service Broker 경로|  
|21587|통계|  
|21825<br /><br /> 21827<br /><br /> 21831<br /><br /> 21843<br /><br /> 21847|사용자|  
|22099|Service Broker 서비스|  
|22601|인덱스|  
|22604|인증서 로그인|  
|22611|XMLSchema|  
|22868|Type|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
