---
title: sysmergeschemachange (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4cfc7662dc9ef63d606c0fae39713c1a012b5a0d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  스냅숏 에이전트가 생성한 게시된 아티클에 대한 정보를 포함합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|게시의 ID입니다.|  
|**artid**|**uniqueidentifier**|아티클의 ID입니다.|  
|**스키마 버전**|**int**|마지막 변경한 스키마의 번호입니다.|  
|**schemaguid**|**uniqueidentifier**|마지막 스키마의 고유한 ID입니다.|  
|**schematype**|**int**|스키마 변경 유형입니다.<br /><br /> **-1** = 유효 하지 않습니다.<br /><br /> **1** = SQL 명령입니다.<br /><br /> **2** = 스키마 스크립트입니다.<br /><br /> **3** = 네이티브 대량 복사 프로그램 유틸리티 (BCP).<br /><br /> **4** = character BCP 합니다.<br /><br /> **5** = 마지막 기록 된 생성 합니다.<br /><br /> **6** = 마지막으로 보낸 생성 합니다.<br /><br /> **7** = 디렉터리입니다.<br /><br /> **8** = 우선 순위입니다.<br /><br /> **9** = 보존 기간입니다.<br /><br /> **10** = 트리거 스크립트입니다.<br /><br /> **11** = 테이블 변경 합니다.<br /><br /> **12** = 모두 다시 초기화 합니다.<br /><br /> **13** = ALTER TABLE (비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).<br /><br /> **14** = 업로드로 다시 초기화 합니다.<br /><br /> **15** = 제약 조건 및 인덱스 스크립트입니다.<br /><br /> **16** = 메타 데이터 정리 합니다.<br /><br /> **17** = 마지막으로 보낸 생성 업데이트 합니다.<br /><br /> **18** = 이전 버전과 호환성 수준입니다.<br /><br /> **19** = 구독자 정보 유효성 검사 합니다.<br /><br /> **20** = 올바르게 분할 합니다.<br /><br /> **21** = 사용자 지정 해결 합니다.<br /><br /> **22** = 아티클 처리 순서입니다.<br /><br /> **23** = 트랜잭션 게시에 게시 합니다.<br /><br /> **24** = 오류 보정 합니다.<br /><br /> **25** = 대체 스냅숏 폴더.<br /><br /> **26** = 다운로드 전용입니다.<br /><br /> **27** = 삭제 추적 합니다.<br /><br /> **40** = 사전 생성 스냅숏 스크립트입니다.<br /><br /> **45** = 사후 생성 스냅숏 스크립트입니다.<br /><br /> **46** = 주문형 사용자 스크립트입니다.<br /><br /> **50** = 스냅숏 헤더 시작 합니다.<br /><br /> **51** = 스냅숏 헤더 끝입니다.<br /><br /> **52** = 스냅숏 트레일러 합니다.<br /><br /> **53** = 프로토콜 FTP (파일 전송) 주소입니다.<br /><br /> **54** = FTP 포트입니다.<br /><br /> **55** = FTP 하위 디렉터리입니다.<br /><br /> **56** = 스냅숏 압축 합니다.<br /><br /> **57** = FTP 로그인 합니다.<br /><br /> **58** = FTP 암호입니다.<br /><br /> **60** = 시스템 사전 생성 스크립트입니다.<br /><br /> **61** = 저장 프로시저 스키마입니다.<br /><br /> **62** = 뷰 스키마입니다.<br /><br /> **63** = 사용자 정의 함수 스키마입니다.<br /><br /> **64** = 뷰 인덱스입니다.<br /><br /> **65** = 확장 속성입니다.<br /><br /> **66** = 유효성을 검사 합니다.<br /><br /> **67** = 프리 스냅숏 SQL 명령입니다.<br /><br /> **71** = 동적 스냅숏 유효성을 검사 합니다.<br /><br /> **80** = 시스템 테이블 기본 BCP 9.0입니다.<br /><br /> **81** = 시스템 테이블 문자 BCP 9.0입니다.<br /><br /> **82** = 시스템 테이블 기본 BCP 9.0 (전역만 해당).<br /><br /> **83** = 시스템 테이블 문자 BCP 9.0 (전역만 해당).<br /><br /> **84** = 시스템 테이블 기본 BCP 9.0 (경량).<br /><br /> **85** = 시스템 테이블 문자 BCP 9.0 (경량).<br /><br /> **128** = 동적 BCP (비트)입니다.<br /><br /> **131** = 동적 기본 BCP 합니다.<br /><br /> **132** = 동적 문자 BCP 합니다.<br /><br /> **208** = 동적 시스템 테이블 기본 BCP 9.0입니다.<br /><br /> **209** = 동적 시스템 테이블 문자 BCP 9.0입니다.<br /><br /> **210** = 동적 시스템 테이블 기본 BCP 9.0 (전역만 해당).<br /><br /> **211** = 동적 시스템 테이블 문자 BCP 9.0 (전역만 해당).<br /><br /> **212** = 동적 시스템 테이블 기본 BCP 9.0 (경량).<br /><br /> **213** = 동적 시스템 테이블 문자 BCP 9.0 (경량).<br /><br /> **300** = 데이터 정의 언어 (DDL) 동작 합니다.<br /><br /> **1024** = 증분 스냅숏 제어 합니다.<br /><br /> **1049** = 증분 스냅숏 폴더.<br /><br /> **1074** = 증분 스냅숏 시작 헤더입니다.<br /><br /> **1075** = 증분 스냅숏 끝 헤더입니다.<br /><br /> **1076** = 증분 스냅숏 트레일러 합니다.<br /><br /> **1077** = 증분 FTP 주소입니다.<br /><br /> **1078** = 증분 FTP 포트입니다.<br /><br /> **1079** = 증분 FTP 하위 디렉터리입니다.<br /><br /> **1080** = 증분 압축된 스냅숏 합니다.<br /><br /> **1081** = 증분 FTP 로그인 합니다.<br /><br /> **1082** = 증분 FTP 암호입니다.|  
|**schematext**|**nvarchar(2000)**|스크립트 파일의 이름 또는 파일 이름이 포함된 명령입니다.|  
|**schemastatus**|**tinyint**|아티클에 대해 스키마 변경 내용이 보류 중인지 여부를 나타내며 값은 다음 중 하나입니다.<br /><br /> **0** = 비활성입니다.<br /><br /> **1** = 활성 합니다.<br /><br /> 스키마 변경이 보류 중임을이 값으로 설정 됩니다 **1**합니다.|  
|**schemasubtype**|**int**|스키마 변경의 하위 유형입니다.<br /><br /> **1** ADDCOLUMN =<br /><br /> **2** DROPCOLUMN =<br /><br /> **3** ALTERCOLUMN =<br /><br /> **4** ADDPRIMARYKEY =<br /><br /> **5** ADDUNIQUE =<br /><br /> **6** ADDREFERENCE =<br /><br /> **7** DROPCONSTRAINT =<br /><br /> **8** ADDDEFAULT =<br /><br /> **9** ADDCHECK =<br /><br /> **10** DISABLETRIGGER =<br /><br /> **11** ENABLETRIGGER =<br /><br /> **12** DISABLETRIGGER =<br /><br /> **13** ENABLETRIGGER =<br /><br /> **14** ENABLECONSTRAINT =<br /><br /> **15** DISABLECONSTRAINT =<br /><br /> **16** ENABLECONSTRAINT =<br /><br /> **17** DISABLECONSTRAINT =|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
