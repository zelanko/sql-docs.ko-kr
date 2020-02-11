---
title: sysmergeschemachange (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
author: stevestein
ms.author: sstein
ms.openlocfilehash: e7225fae192ab256c2c2660fcb1554cd01818907
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029824"
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  스냅샷 에이전트가 생성한 게시된 아티클에 대한 정보를 포함합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|게시의 ID입니다.|  
|**artid**|**uniqueidentifier**|아티클의 ID입니다.|  
|**schemaversion**|**int**|마지막 변경한 스키마의 번호입니다.|  
|**schemaguid**|**uniqueidentifier**|마지막 스키마의 고유한 ID입니다.|  
|**schematype**|**int**|스키마 변경 유형입니다.<br /><br /> **-1** = 잘못 되었습니다.<br /><br /> **1** = SQL 명령입니다.<br /><br /> **2** = 스키마 스크립트<br /><br /> **3** = 네이티브 대량 복사 프로그램 유틸리티 (BCP)<br /><br /> **4** = 문자 BCP<br /><br /> **5** = 마지막으로 기록 된 세대입니다.<br /><br /> **6** = 마지막으로 보낸 세대입니다.<br /><br /> **7** = 디렉터리입니다.<br /><br /> **8** = 우선 순위.<br /><br /> **9** = 보존 기간<br /><br /> **10** = 트리거 스크립트<br /><br /> **11** = Alter table<br /><br /> **12** = 모두 다시 초기화<br /><br /> **13** = ALTER TABLE (비[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])<br /><br /> **14** = 업로드를 사용 하 여 다시 초기화<br /><br /> **15** = 제약 조건 및 인덱스 스크립트<br /><br /> **16** = 메타 데이터 정리.<br /><br /> **17** = 마지막으로 보낸 생성을 업데이트 합니다.<br /><br /> **18** = 이전 버전과의 호환성 수준<br /><br /> **19** = 구독자 정보의 유효성을 검사 합니다.<br /><br /> **20** = 잘 분할 되었습니다.<br /><br /> **21** = 사용자 지정 해결 프로그램.<br /><br /> **22** = 아티클 처리 순서<br /><br /> **23** = 트랜잭션 게시에 게시 됩니다.<br /><br /> **24** = 오류를 보정 합니다.<br /><br /> **25** = 대체 스냅숏 폴더입니다.<br /><br /> **26** = 다운로드 전용.<br /><br /> **27** = 추적 삭제<br /><br /> **40** = 미리 생성 된 스냅숏 스크립트<br /><br /> **45** = 생성 후 스냅숏 스크립트<br /><br /> **46** = 주문형 사용자 스크립트<br /><br /> **50** = 스냅숏 헤더를 시작 합니다.<br /><br /> **51** = 스냅숏 헤더 끝입니다.<br /><br /> **52** = 스냅숏 트레일러<br /><br /> **53** = 파일 전송 프로토콜 (FTP) 주소입니다.<br /><br /> **54** = FTP 포트<br /><br /> **55** = FTP 하위 디렉터리입니다.<br /><br /> **56** = 스냅숏이 압축 되었습니다.<br /><br /> **57** = FTP 로그인<br /><br /> **58** = FTP 암호<br /><br /> **60** = 시스템 사전 생성 스크립트<br /><br /> **61** = 저장 프로시저 스키마.<br /><br /> **62** = 뷰 스키마<br /><br /> **63** = 사용자 정의 함수 스키마입니다.<br /><br /> **64** = 인덱스를 봅니다.<br /><br /> **65** = 확장 속성<br /><br /> **66** = 유효성을 검사 합니다.<br /><br /> **67** = 프리 스냅숏 SQL 명령입니다.<br /><br /> **71** = 동적 스냅숏 유효성 검사<br /><br /> **80** = 시스템 테이블 기본 BCP 9.0.<br /><br /> **81** = 시스템 테이블 문자 BCP 9.0.<br /><br /> **82** = 시스템 테이블 기본 BCP 9.0 (전역 전용)<br /><br /> **83** = 시스템 테이블 문자 BCP 9.0 (전역 전용)<br /><br /> **84** = 시스템 테이블 기본 BCP 9.0 (경량).<br /><br /> **85** = 시스템 테이블 문자 BCP 9.0 (경량).<br /><br /> **128** = 동적 BCP (비트)입니다.<br /><br /> **131** = 동적 네이티브 BCP.<br /><br /> **132** = 동적 문자 BCP<br /><br /> **208** = 동적 시스템 테이블 기본 BCP 9.0.<br /><br /> **209** = 동적 시스템 테이블 문자 BCP 9.0.<br /><br /> **210** = 동적 시스템 테이블 기본 BCP 9.0 (전역 전용)<br /><br /> **211** = 동적 시스템 테이블 문자 BCP 9.0 (전역 전용)<br /><br /> **212** = 동적 시스템 테이블 기본 BCP 9.0 (경량).<br /><br /> **213** = 동적 시스템 테이블 문자 BCP 9.0 (경량).<br /><br /> **300** = DDL (데이터 정의 언어) 작업<br /><br /> **1024** = 증분 스냅숏 컨트롤입니다.<br /><br /> **1049** = 증분 스냅숏 폴더입니다.<br /><br /> **1074** = 증분 스냅숏 시작 헤더입니다.<br /><br /> **1075** = 증분 스냅숏 끝 헤더입니다.<br /><br /> **1076** = 증분 스냅숏 트레일러<br /><br /> **1077** = 증분 FTP 주소<br /><br /> **1078** = 증분 FTP 포트<br /><br /> **1079** = 증분 FTP 하위 디렉터리입니다.<br /><br /> **1080** = 증분 압축 스냅숏<br /><br /> **1081** = 증분 FTP 로그인<br /><br /> **1082** = 증분 FTP 암호|  
|**schematext**|**nvarchar (2000)**|스크립트 파일의 이름 또는 파일 이름이 포함된 명령입니다.|  
|**schemastatus**|**tinyint**|아티클에 대해 스키마 변경 내용이 보류 중인지 여부를 나타내며 값은 다음 중 하나입니다.<br /><br /> **0** = 비활성<br /><br /> **1** = 활성<br /><br /> 스키마 변경이 보류 중인 경우이 값은 **1**로 설정 됩니다.|  
|**schemasubtype**|**int**|스키마 변경의 하위 유형입니다.<br /><br /> **1** = addcolumn<br /><br /> **2** = dropcolumn<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = addprimarykey<br /><br /> **5** = addunique<br /><br /> **6** = addreference<br /><br /> **7** = dropconstraint<br /><br /> **8** = adddefault<br /><br /> **9** = addcheck<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
